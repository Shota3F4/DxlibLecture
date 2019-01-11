# Dxlibの基本関数  
## 基本関数の説明
**SampleGame→SampleGame.sln**を開いてください。  
test.txtに書かれているこのプログラムをみてください。
```C++
int WINAPI WinMain(HINSTANCE,HINSTANCE,LPSTR,int){
    changeWindouMode(true); 
    DxLib_Init();
    WaitKey();
    DxLib_End();
    return 0;
}
```

###  DxLib_Init();
Dxlibを使う際、必ず呼ぶ関数です。  
これを呼ぶことでDxlibの初期化を行っています。
### WaitKey();
何かキーが押されるまで処理をストップする関数です。  
ストップしている間はあらゆる関数を呼ぶことができません。
(処理を強制的に止めるので普通は使われません。)
### DxLib_End();
Dxlibを使用したプログラムを終了するとき、必ず呼ばれる関数です。
### ChangeWindowMode(bool);
Windowモードにするか、全画面モードにするかを選択します。  
boolの値が  
true:Windowモード  
false:全画面モード(デフォルト)  
**※この関数はDxlib_Init()より前に呼ばないといけません**


## ChangeWindowMode()について

- もしChangeWindowMode()関数を呼ばないとどうなるでしょう。

```C++
int WINAPI WinMain(HINSTANCE,HINSTANCE,LPSTR,int){
    //changeWindowModeをコメントアウトした
    //changeWindowMode(true); 
    DxLib_Init();
    WaitKey();
    DxLib_End();
    return 0;
}
```
コンパイルして実行してみましょう。  
恐らく画面全体が黒くなり、何かキーを押すと元に戻るようになったはずです。  
これで、changeWindowMode(bool)を呼ばない場合、全画面になる事が分かったと思います。
***
- もしChangeWindowMode()関数をDxlib_Init()の後に呼ぶとどうなるでしょう。

```C++
int WINAPI WinMain(HINSTANCE,HINSTANCE,LPSTR,int){
    //Dxlib_Initが前に来た
    DxLib_Init();
    changeWindowMode(true); 
    WaitKey();
    DxLib_End();
    return 0;
}
```
コンパイルして実行してみましょう。  
恐らくまた画面全体が黒くなり、何かキーを押すと元に戻るようになったはずです。  
これで、changeWindowMode(bool)をDxlib_Init()の後に呼んでも意味がない事が分かったと思います。

****
実はDxlib_Init()関数は、Dxlibの初期化をすると同時に、Window生成、フォントデータの生成、サウンドの準備等を行っています。  
つまり、Dxlib_Init()でWindow生成を済ませた後のタイミングではWindowに関する設定はできません。(適応できないため)  
なので、ChangeWindowMode()関数はDxlib_Init()より前で呼ぶ必要があり、またDxlib_Init()の後で呼んでも適応されることが分かります。  
このことから、Windowの設定に関する関数はDxlib_Init()よりも前で呼ぶ必要があります。  
たとえば、  
SetWindowText(char)...windowの上に表示される名前を変更する   
SetWindowIconID(int)...Windowのアイコンを変更する  
これらの関数もChangeWindowMode()と同じようにDxlib_Init()より前によぶ必要があります  
いつか使うと思いますので、ここでは説明はしません
*******
*****
## おまけ
### もしChangeWindowMode()関数をDxlib_Init()の後に呼んだ後、一度DxLib_End()を呼びだして終了し、またDxlib_Init()を呼び出すと...？
```C++
int WINAPI WinMain(HINSTANCE,HINSTANCE,LPSTR,int){
    //一度目のDxlib_Init()
    DxLib_Init();
    //ここで変えた(二度目に影響が出るのかどうか)
    ChangeWindowMode(true); 
    WaitKey();
    DxLib_End();

    //二度目のDxlib_Init()
    DxLib_Init();
    WaitKey();
    DxLib_End();
    return 0;
}
```
実行すると、**一度全画面モードになり、その後何かキーを押すと今度はWindowモードになる**ことが確認できるでしょうか。  
一度目と二度目のDxlib_Init()で生成されるWindowが変わっています。なぜ変わったのでしょうか？  
一度目の時はWindowモードがデフォルトの全画面モードのまま生成され、その後Windowモードをスクリーンモードにする処理を実行、その後改めて今度はスクリーンモードでWindowを生成しなおしているからです。
