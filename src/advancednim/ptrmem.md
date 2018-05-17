# ポインタとメモリ

[参照セクション](/ref)では、基本的なポインタの説明と`ref`について解説しました。

このセクションでは、`ptr`型のポインタとメモリ管理について解説していきます。

## ポインタとメモリ

## デストラクタ

## ガベージコレクション
私達は、プログラムを書く上で何らかの値は必ず変数に代入しています。

この変数はコンピュータから見るとメモリ内のどこかにあるように見え、その場所がアドレスとなっています。

メモリの管理はOSが管理していて、私達が変数に値を入れる時、プログラムは内部でOSからメモリを借りることによって値を入れる場所を確保できるのです。

今メモリを**借りる**という表現をしました。

これは借り終わったら返さないといけないことを意味します。

では私達は借りたメモリをどのように返すのでしょうか？

例えばC言語のような言語では`free`と呼ばれる関数に返すメモリのポインタを渡してコールすることで手動で返すことをしています。

しかし、今までNimを書いてきていて`free`に価するようなプロシージャはあったでしょうか？

ここで出てくるのがガベージコレクションです。

ガベージコレクションとは、直訳するとゴミ収集ですがその意味の通り、自動で使われなくなったリソースを回収し、解放してくれる機能のことを言います。

Nimにはこのガベージコレクションが実装されており、基本的に私達がOSにメモリを返すようなことはしなくていいようになっています。

Nimのガベージコレクションは`ref`型のポインタを監視していていますが、このセクションで紹介する`ptr`型は監視していません。

そのため、`ptr`型のポインタとして確保されたメモリは我々プログラマーたちが解放して上げる必要があります。

通常、Nimにおいて手動でメモリ管理をすることはあまりないですが、低レベルでの最適化やCなどとの連携で必要になる場合があります。

Nimに実装されているGCのは複数あり、どれも効率的に実装されています。

GCの切り替えはコンパイルオプションで`--gc:GC名`とすることで切り替えることが出来ます。

- `refc`

デフォルトのGC。コンパイル時に指定しないとこのGCになる。遅延参照カウントによってGCを行う。
スタック上の参照はCコード生成とパフォーマンスのためにカウントされません。

- `markAndsweep`
単純なマーク&スウィープのGC。

- `v2`

インクリメンタルマーク&スウィープGC。まだ完全な実装ではないようで、使用時には注意が必要です。

- `boehm`

単純なboehmGC実装。このGCをだけは少し特別で、`ptr`のポインタも追跡するため、手動で確保したメモリも監視対象。
しかし、他のGCと比べてパフォーマンスが悪くなったりする場合がある。

- `go`

Go言語のGC。libgoが必要。

- `none`
GCをオフにする。