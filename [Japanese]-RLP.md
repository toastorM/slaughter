<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

:stop_sign: **This wiki has now been deprecated. Please visit [ethereum.org](https://ethereum.org/ja) for up-to-date information on Ethereum.** :stop_sign: 


**Contents**

- [定義](#%E5%AE%9A%E7%BE%A9)
- [例](#%E4%BE%8B)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

RLPの目的は任意の入れ子構造のバイナリデータ(nested binary data)を符号化することです。
RLPはEthereumにおいてシリアライズされたオブジェクトを符号化する一般的な方法です。
RLPの目的は構造を符号化することです:
特殊なアトミックなデータ型(例えば文字列型、整数型、浮動小数点型)の符号化はもっと上位のプロトコルに任せます；
Ethereumでは整数型は先頭のゼロが無いビッグエンディアンのバイナリで表されます
(よって、整数型のゼロは空のバイトアレイとなります)。

もしある辞書を符号化するのにRLPを使いたいと思うならば、
二つの正規のフォームが使えます。
`[[k1,v1],[k2,v2]...]`のような辞書順にならんだキーを使用する方法と、
Ethereumで使用されている上位の[Patricia Tree](https://github.com/ethereum/wiki/wiki/Patricia-Tree)を用いた符号化を使用する方法です。


### 定義

RLP符号化関数はアイテムを受け入れます。アイテムは以下のように定義されます:

* 文字列型(すなわちバイトアレイ)はアイテムである
* アイテムのリストはアイテムである

例えば、空の文字列はアイテムです。同様に "cat"という単語による文字列もアイテムです。任意の個数の文字列型のリストもアイテムです。そして、`["cat",["puppy","cow"],"horse",[[]],"pig",[""],"sheep"]`のようなもっと複雑なデータ構造もアイテムです。この論説の残りの部分の文脈において、"文字列型"は"あるバイト数のバイナリデータ"と同義語であることに注意しましょう; 特殊なエンコードは用いられておらず、文字列型の内容が何を意味しているかの知識は必要ではありません。

RLPエンコーディング(符号化)は以下のように定義されます:

* `[0x00, 0x7f]`の間にある１バイトの値は、そのバイトがそのまま自分自身のRLPエンコーディングとなります。
* もし、文字列が0-55バイトの長さの場合は、RLPエンコーディングは**0x80**と文字列の長さを足した1バイトと、その後に続く文字列で構成されます。よって、最初の1バイトは`[0x80, 0xb7]`の範囲となります。
* もし文字列が55バイトより長い場合、RLPエンコーディングは以下の3つで構成されます。
文字列の長さをバイナリで表した時に必要となるバイト数を**0xb7**に足した値の1バイト。
続けて、文字列の長さ、それに続く文字列です。
例えば1024の長さを持つ文字列の場合、
文字列の表記に10bitつまり2byte必要なので`\xb9`と、1024を表す`\x04 00`により、
`\xb9\x04\x00`となります。
よって、最初の1バイトは`[0xb8, 0xbf]`の範囲となります。
* もし、リストの全ペイロード(すなわち、全てのアイテムを合わせた長さ)が0-55バイトの長さである場合、RLPエンコーディングは、**0xc0**にリストの長さを足した1バイトの値と、それに続くアイテムをRLPエンコーディングして続けたもので構成されます。よって、最初の1バイトの範囲は`[0xc0, 0xf7]`となります。
* もし、リストの全ペイロードの長さが55バイト以上の場合、RLPエンコーディングは以下の構成になります。最初に **0xf7** にペイロードの長さをバイナリで表した時に必要となるバイト数を足した1バイト。続けて、ペイロードの長さ。最後にアイテムをRLPエンコーディングした物を続けたものとなります。よって、最初の1バイトの範囲は`[0xf8, 0xff]`となります。


コードで表すと以下のようになります：

```python
def rlp_encode(input):
    if isinstance(input,str):
        if len(input) == 1 and ord(input) < 128: return input
        else: return encode_length(len(input),128) + input
    elif isinstance(input,list):
        output = ''
        for item in input: output += rlp_encode(item)
        return encode_length(len(output),192) + output

def encode_length(L,offset):
    if L < 56:
         return chr(L + offset)
    elif L < 256**8:
         BL = to_binary(L)
         return chr(len(BL) + offset + 55) + BL
    else:
         raise Exception("input too long")

def to_binary(x):
    return '' if x == 0 else to_binary(int(x / 256)) + chr(x % 256)
```

### 例

文字列 "dog" = [ 0x83, 'd', 'o', 'g' ]

リスト [ "cat", "dog" ] = `[ 0xc8, 0x83, 'c', 'a', 't', 0x83, 'd', 'o', 'g' ]`

空文字列 ('null') = `[ 0x80 ]`

空リスト = `[ 0xc0 ]`

整数 15 ('\x0f') のエンコード = `[ 0x0f ]`

整数 1024 ('\x04\x00') のエンコード = `[ 0x82, 0x04, 0x00 ]`

[ 集合論的表現 ](http://en.wikipedia.org/wiki/Set-theoretic_definition_of_natural_numbers)  `[ [], [[]], [ [], [[]] ] ] = [ 0xc7, 0xc0, 0xc1, 0xc0, 0xc3, 0xc0, 0xc1, 0xc0 ]`

文字列 "Lorem ipsum dolor sit amet, consectetur adipisicing elit" = `[ 0xb8, 0x38, 'L', 'o', 'r', 'e', 'm', ' ', ... , 'e', 'l', 'i', 't' ]`