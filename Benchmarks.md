# Trie

## Common Trie Benchmarks

The point of this is to give a controlled test between clients that reflects typical on-chain situations. We do this by defining a common dataset of key/value pairs for insertion into the trie and root-calculation. There are two modes to reflect the two use cases of the trie in Ethereum:

- Persistent Tries: The secure tries for storage and state. These have their nodes stored permanently in a backing store and, periodically, are updated a number of times before a new root is taken and used in either the receipt or the account's storage_root field.
- Ephemeral Tries: The receipt and transaction tries. These tries do not require that their nodes be stored permanently, but rather are used primarily to determine their root, which is placed in the header under receipts_root and transactions_root fields.

### Persistent Tries

For this benchmark, the dataset is inserted into the trie with root hashes being computed at specific intervals ("era_size"). This number represents the number of update operations per root calculation.

### Ephemeral Tries

For this benchmark, the important thing is to take all data and determine the root; no roots need be computed along the way and there is no assertion that any state used when determining the root be required. In this sense era_size is equivalent to the dataset size.

## Standard Dataset

Sensible implementations may precompute the dataset to avoid the additional burden of SHA3 computation at benchmark time.

```python
from ethereum import trie, db, utils
import time

MIN_COUNT = 32
ROUNDS = 1000
ERA_SIZE = 4
MAX_COUNT = 32
SYMMETRIC = True
a = time.time()
t = trie.Trie(db.EphemDB())
seed = '\x00' * 32

for i in range(ROUNDS):
    seed = utils.sha3(seed)
    mykey = seed[:MIN_COUNT + ord(seed[-1]) % (MAX_COUNT + 1 - MIN_COUNT)]
    if SYMMETRIC:
        t.update(mykey, mykey)
    else:
        seed = utils.sha3(seed)
        myval = seed[-1] if ord(seed[0]) % 2 else seed
        t.update(mykey, myval)
    if i % ERA_SIZE == 0
        seed = t.root()
print time.time() - a 
print t.root_hash.encode('hex')
```

The final trie root after 1000 rounds should be `36f6...93a3` for `SYMMETRIC = True` and `da8a...0ca4` for `False`.


## Method

Tests run on:
```
Linux gav-MacBookPro 4.4.0-040400rc7-lowlatency #201512272230 SMP PREEMPT Mon Dec 28 03:36:57 UTC 2015 x86_64 x86_64 x86_64 GNU/Linux
```

CPU:
```
model name	: Intel(R) Core(TM) i7-4980HQ CPU @ 2.80GHz
cpu MHz		: 3195.609
cache size	: 6144 KB
bogomips	: 5587.06
```

### C++

```
cd libweb3core
cmake -DCMAKE_BUILD_TYPE=Release
make -j8
sudo nice -n -19 ./libweb3core/bench/bench trie
```

### Parity

```
cd util && cargo bench
```

### CPython / PyPy
```
pip install ethereum
wget https://gist.github.com/heikoheiko/0fa2b322560ba7794f22
python trie_benchmark.py
pypy trie_benchmark.py
```

### Go

```
sudo nice -n -19 godep go test  -run=- -bench=Std ./trie
```

### JS
```
git clone https://github.com/ethereumjs/merkle-patricia-tree.git`
cd merkle-patricia-tree
npm install
node ./benchmarks/random.js
```

## Results

All times in ms.

Test ID is given as `pair_count`-`era_size`-`key_size`-`value_type`, where valid `value_type`s are `ran` (`SYMMETRIC = False`) and `mir` (`SYMMETRIC = True`).

### Persistent Trie Benchmark

The standard secure-trie test is `1k-9-32-ran`. `ran` is used as `value_type` as it better reflects the kinds of values that are typically written in the blockchain. The `9` that is used as `era_size` is determined empirically from the Frontier mainnet: the mean number of insertions per commit on all secure tries from block #0 to #900,000 is 9.35 (TODO: determine median & quartiles - they're likely to be better indicators on real world performance).

| Client      | Time | SHA3s |
| ----------- | --------- | ----- |
| C++ | 23.8 | 8469 |
| CPython | 369 | 7079 |
| PyPy | 45 | |
| Go | 23.6 | |
| Pure JS | 374 | |
| Parity | 11.6 | 4221 |

#### Other results (values other than 9 inserts/commit)

| Test ID      | C++  | CPython | PyPy | Go  | JS  |
| ------------ | ------ | ----- | --- | ---- | --- |
| 1k-3-32-ran  | 23.8   | 369   | 45 | 45.7  | 388 |
| 1k-5-32-ran  | 23.8   | 369   | 41 | 28.5  | 374 |

## Ephemeral Trie Benchmark

For this benchmark, 1k inserts is quite reasonable; we naturally avoid doing any "partially-complete" root determination. TODO: redo benchmarks with two byte key size & 32-byte value size to better reflect the insecure trie contents.

| Test ID      | C++  | CPython | PyPy | Go  | JS  | Parity |
| ------------ | ------ | ----- | --- | ---- | --- | ------ |
| 1k-1k-32-ran | 23.8   | 369   | 46 | 10.0  | 389 | 1.634  |
| 1k-1k-32-mir | 23.9   | 294   | 45 | 8.0   | 382 | 1.529  |

Note: PyPy times were measured on 1.7 GHz i7