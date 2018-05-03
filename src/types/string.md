# 文字列型

* 文字列 `string`, `cstring`

`string`はNimで使われる通常の文字列型です。文字列型は`char`型の配列なので、`[]`演算子とインデックス数値で任意のポジションの文字を取得できます。

例えば `str[0 .. 2]` は `str` 0 文字目から 2 文字目、つまり `str` が "Nim World" ならば "Nim" を返します。

`cstring`は主にCとの連携で使う文字列型で、Cにおいて`char *`と同じものを意味します。

内部的にはGCの回収対象で、回収されてしまうことがありますが、GCはスタックのルートを控えめに監視しているので、ほぼ回収されることはありません。

ですが、もし問題が起きる場合は`GC_ref`や`GC_unref`を使用してGC回収を防ぐことができます。

```nim
var
  str = "Hello, World!"
  cstr: cstring = "Hello, World!"

echo str[0] # H
echo str[0 .. str.len - 2] # Hello, World
```