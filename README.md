-----------------------------------
#Androidアプリのプログラムに挑戦  
ボタン押下時の処理  
-----------------------------------

![14](https://github.com/miyake-yasunaga/02_Button/blob/master/images/14.png)

｢Hello world｣ の文字を｢こんにちは｣に  
変えることができましたが、  

よく考えたらＸＭＬファイルをさわっただけで  
javaのプログラム自体はまだ全然変更してませんね。  

では、いよいよプログラムで文字を表示させるのに  
挑戦してみましょう！  

画面にボタンを追加して、ボタンを押すと  
｢さようなら｣という表示が変わるようにしてみましょう。  

今回はＸＭＬをコードで書かずにＧＵＩで編集してみます。  

Projectのファイル一覧から｢activity_main.xml｣を選択して  
中央下に表示されてる  

｢Design｣のタブをクリックしてＧＵＩ画面を表示します。  

![01](https://github.com/miyake-yasunaga/02_Button/blob/master/images/01.png)


｢Widgets｣の下の方にある｢Button｣を選択した状態で  
右のAndroid画面にマウスを移動させて適当な場所でクリックします。  

![02](https://github.com/miyake-yasunaga/02_Button/blob/master/images/02.png)

画面にボタンが追加されました。  

![03](https://github.com/miyake-yasunaga/02_Button/blob/master/images/03.png)

中央下に表示されてる  
｢Text｣のタブをクリックしてＧＵＩ画面を表示します。  

ボタンウィジェットの記述が追加されています。  

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="New Button"
        android:id="@+id/button"
        android:layout_below="@+id/textView"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="149dp" />

・・・？  
よく見ると  
        android:text="New Button"  
の行に色がついてます。  

![04](https://github.com/miyake-yasunaga/02_Button/blob/master/images/04.png)

ここにマウスを近づけると  
吹きだしが出てきました。  

｢固定の文字はソースの中に直接書かずに｢string.xml｣に書くべだ｣  
と言ってるようです。  

![05](https://github.com/miyake-yasunaga/02_Button/blob/master/images/05.png)

言われた通りに  
｢string.xml｣を選択して、  
ボタンに表示させる文字（button01）と  
ボタンをクリックした時に表示する文字（message01）を設定します。  

![06](https://github.com/miyake-yasunaga/02_Button/blob/master/images/06.png)

｢activity_main.xml｣を選択して  

android:text="New Button"  
↓↓↓  
android:text="@string/button01"  
に変更します。  

右側画面イメージのボタン表示も｢string.xml｣に設定した文字に変わりました。  
これでＸＭＬの準備は終わりました。  


![08](https://github.com/miyake-yasunaga/02_Button/blob/master/images/08.png)

いよいよjavaのコーディングです。  

｢MainActivity.java｣を選択します。  

処理の動きとしては  
画面の表示後にボタン押下した場合の処理を追加するので  

    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

の下に書いていきます。  

どのボタンを制御するかということで  
Button型の変数をbtn01という名前で宣言して  
先ほどxmlに追加したボタンのidを指定します。  

        Button btn01 = (Button) this.findViewById(R.id.button);

すると、また吹き出しが出て来ました・・・  
｢Buttonって書いてるけど、なんの事？  
android.widget.Buttonを使いたいならをAlt+Enter押してパッケージをimportしてね ｣  

という事みたいです。  

![09](https://github.com/miyake-yasunaga/02_Button/blob/master/images/09.png)

言われた通りAlt+Enterを押します。  

         import android.widget.Button;  
が追加されました。  

![10](https://github.com/miyake-yasunaga/02_Button/blob/master/images/10.png)

ボタンクリック時の処理を追加します。  

        btn01.setOnClickListener(new View.OnClickListener() {

という1行を追加すると下記のソースが自動で表示されます。  
ここのonClickに処理を書きます。  

            @Override  
            public void onClick(View v) {  

            }  

![11](https://github.com/miyake-yasunaga/02_Button/blob/master/images/11.png)

先ほどのボタンと同じようにテキストも  
TextView型の変数をtv01という名前で宣言して  
xmlに設定している｢さようなら｣を表示しているtext表示のidを指定します。  

        final TextView tv01 = (TextView)this.findViewById(R.id.textView);  

あとはonClick時に、上で記述した変数tv01に  
｢string.xml｣のmessage01に設定した文字をセットするという記述をすれば完成です。  


            public void onClick(View v) {  

                tv01.setText(R.string.message01);　←この1行を追加  

            }  

ボタンと同じように  
         import android.widget.TextView;  
も追加されました。  

これでメニューの三角ボタンでビルドすると・・・

![12](https://github.com/miyake-yasunaga/02_Button/blob/master/images/12.png)

ボタンが表示されました。  

ボタンをクリックすると・・・  

![13](https://github.com/miyake-yasunaga/02_Button/blob/master/images/13.png)

｢さようなら｣の文字が  
｢ボタンが押されました！｣  
に変わりました！  

![14](https://github.com/miyake-yasunaga/02_Button/blob/master/images/14.png)

整理すると  

MainActivity.に処理を記述  
activitymain.xmlに画面レイアウトを記述  
strings.xmlに文字情報を記述  

という仕組みのようです。  

慣れないとややこしそうですが、  
役割ごとにファイルを分けてるので  
処理が複雑になってきても  
ソースは結構見やすいかもしれませんね。  
