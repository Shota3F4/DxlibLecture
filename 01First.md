# 1.DXライブラリってなんだよ
皆さんは今まで，  
``` C
 #include <stdio.h>

int main(){
        printf("hello");
        return 0;
}
```
こんなコードを書いたことがあると思います．
実行すると，  
!["実行結果"](Image/01helloResult.png )  
こうなりますよね．  
このような，黒い画面をコンソール画面といいます．  
皆さんはこれまで，コンソール画面に文字出力をしたことは何度も何度もあると思います．  
ではこれをどう使ったらゲームやアプリを作れるのでしょう？  

実は，コンソール画面からゲームを作るのはとても困難です．苦行です．  
更に言えば，C言語そのものではゲームを作ることなんてできやしません．  
ここでいうそのものとは，何も `#include`していない状態のものです  
上のソースコードでは`stdio.h`が`include`されています．
この`stdio.h` とは，標準入出力関数ライブラリと言われ，入力やコンソール画面に出力するための関数を集めたものです．  
この中にある`printf()`関数を使うことで皆さんはコンソール画面に出力できていたわけですね.   

ということで標準のC言語ではWindowを生成することも，画像を扱うこともできません．ゲームなんて到底作れません．  
そこで登場するのが*DXライブラリ*です！！！！！  
DXライブラリならWindow生成も簡単で画像操作も分かりやすいです  
先ほどの`stdio.h`が標準入出力関数ライブラリなら，DXライブラリは標準ゲームライブラリといったところです．ゲームに関する，基本的な機能を保証してくれています．  
ライブラリを使用するためには，先頭に  
 `#include <DxLib.h>`  
と書くだけです．(前にいろいろやることはありますが)
***
***
## さらに
実は，DXライブラリはDirectXというライブラリを分かりやすく簡易化してくれたものです．  
>DirectXとは， Microsoft DirectX（ダイレクトエックス）は、マイクロソフトが開発したゲーム・マルチメディア処理用のAPIの集合である[1]。  
オーバーヘッドを少なくしたデバイスの仮想化・抽象化を提供する。Windows・Xbox・Xbox 360・Xbox Oneなど、マイクロソフト製のプラットフォームおよびデバイスにおいて広く利用されている。グラフィックスに関しては、DirectX (Direct3D) 互換のビデオカードを利用することにより、高品質の2次元・3次元コンピュータグラフィックスを高速にレンダリングできる.
>>Wikipedia Microsoft DirectXより

じゃあ，DXライブラリなんかやめて，DirectXやろうぜ！！ と思った人もいると思います．  
それではなぜ，DirectXを簡易化したライブラリなんてあるのでしょうか？  
答えは簡単，DirectXの習得がとてつもなく困難だからです.   
DXライブラリはそんなDirectXをゲーム開発初心者でも分かりやすくしてくれたものになってます．  
DXライブラリの学習が大体終わった人はDirectXにも挑戦してみるといいかもしれません．  