
## 数式の全体像を確認
では始めに数式の全体像を確認しましょう。まず、下の表は前のページでも紹介したものです。
![1](https://user-images.githubusercontent.com/45871453/59075520-fcc62380-890b-11e9-89f2-d09b0553b01b.jpg)

この例では「部署名」が総務部のデータのみを抜き出しています。そしてこの中で、セルA１５に入れた数式は次の通りです。

### 【セルA15の数式】

    {=IFERROR(INDEX($A$3:$G$8,MATCH(

    LARGE(($F$3:$F$8="総務部")*1/ROW($A$3:$A$8),ROWS($A$15:$A15)),

    1/ROW($A$3:$A$8),0),COLUMNS($A$14:A$14)),"")}


このように全部で８個、７種類の関数を使います。正直慣れるまでは大変ですが、使いこなせるようになると便利ですので、順番にやってみましょう。

なお、下のように「数式バー」と呼ばれる所へ手で入力していくと楽なので、その手順で説明します。

### ### IFERROR関数とINDEX関数の部分
では始めの「IFERROR」と「INDEX」の部分です。

手で**「＝IFERROR(INDEX( 」** と入力します。

そしてカッコの次に入力するのは**「タイトル行を除く元の表全ての範囲」** です。

![2](https://user-images.githubusercontent.com/45871453/59075708-1caa1700-890d-11e9-9fff-41bd3132825b.jpg)

ここでデータが入っている部分、つまり「Ａ３～Ｇ８」までを指定し、「,（コンマ）」を入れます。

【入力した数式】


    =IFERROR(INDEX($A$3:$G$8,


ちなみに「＄」マークは付けた状態にしてください。

### MATCH関数＋LARGE関数の部分

次は、下のように**「MATCH(LARGE((」** と入力します。

![3](https://user-images.githubusercontent.com/45871453/59075749-4a8f5b80-890d-11e9-9022-e0e89fc1ce46.jpg)

そして次に入力するのは、**「条件を指定したい１列の範囲とその条件」** です。

ここでは、「部署名」が入ったF列の３～８行目に対して「総務部のみ」という条件で抽出したいので「$F$3:$F$8=”総務部”」となります。

![4](https://user-images.githubusercontent.com/45871453/59075793-82969e80-890d-11e9-8cf3-b6ef705b5ecb.jpg)

普通は「F3="総務部"」のように、一つのセルに対して指定しますがここではこのように複数の範囲を指定してください。

ちなみに条件を、もし「部署名を総務部以外」としたければ「$F$3:$F$8<>”総務部”」、「役職を課長のみ」としたければ「$G$3:$g$8=”課長”」となります。

そして指定したい条件が１つであれば、その後に「*1」と入力します。すると数式は下のようになります。


【入力した数式】

    =IFERROR(INDEX($A$3:$G$8,MATCH(LARGE(($F$3:$F$8="総務部")*1

なお、付けたい条件が複数、例えば「F列が総務部」で「G列が課長」のデータを抜き出したいのであれば、ここは「～LARGE（$F$3:$F$8=”総務部”）*（$G$3:$G$8=”課長”）」などと、条件を「*」で繋いで入力します。

この場合数式は次のようになります。

【複数条件の場合の数式の例】

    =IFERROR(INDEX($A$3:$G$8,MATCH(LARGE(($F$3:$F$8="総務部")*($G$3:$G$8)="課長"

### ROW関数の部分
![5](https://user-images.githubusercontent.com/45871453/59075823-a78b1180-890d-11e9-9fbd-7225a132ef5e.jpg)


そしてＲＯＷのカッコ内には、「どこの列でもいいのでデータが入っている１列の範囲」を選択します。

例でデータが入っている行は「３～８行目」だったので、ここは**「$A$3:$A$8」** とし、その後に**「 ),」** （←カッコ１つとコンマ）を付けています。

![6](https://user-images.githubusercontent.com/45871453/59075836-bd003b80-890d-11e9-847c-87c43adae68f.jpg)

この時３～８行目であれば、B行（「$B$3:$B$8」）でもX行（「$X$3:$X$8」）でも、どこの列でも構いません。

すると数式は下のようになります。

【入力した数式】

    「=IFERROR(INDEX($A$3:$G$8,MATCH(LARGE(($F$3:$F$8="総務部")*1/ROW($A$3:$A$8),」

### ROWS関数の部分

続いて**「ROWS($A$15:$A15)),」** と入力してください。

このROWSで指定する範囲も、列番号はどこでも構いません。B列でもD列でもZ列でも、どこでもいいです。

また、行番号も「1」でも「6」でも「99574」でも、どこでも構いません。

ただしここで気を付けることは、

① 「：」の前のセル番号には「$」を２つ（例では「$A$15」）、「：」の後のセル番号には「$」を前に一つ（例では「$A15」）付けること

② 「：」の前と後のセル番号は同じにすること（例では「：」の前も後も同じ「A15」）

の２つです。

すると下のようになります。

【入力した数式】

    「=IFERROR(INDEX($A$3:$G$8,MATCH(LARGE(($F$3:$F$8="総務部")*1/ROW($A$3:$A$8),ROWS($A$15:$A15)), 」

そして次に **「1/」** と入力。

その後に「 ** ROW( ** 」と入力し、カッコ内は先ほどのROW関数のところと同じように「どこの列でもいいのでデータが入っている行の範囲（例では「 ** $A$3:$A$8 ** 」）」を入れます。

そして「 ** ),0), ** 」（←カッコ、コンマ、ゼロ、カッコ、コンマ）と入れると、数式は下のようになります。

![7](https://user-images.githubusercontent.com/45871453/59075862-dd2ffa80-890d-11e9-8c9c-b8ec48de8f24.jpg)

【入力した数式】

    「=IFERROR(INDEX($A$3:$G$8,MATCH(
      LARGE(($F$3:$F$8="総務部")*1/ROW($A$3:$A$8),ROWS($A$15:$A15)
      ),1/ROW($A$3:$A$8),0),」


### COLUMNS関数の部分

最後に **「COLUMNS($A$14:A$14)),””)」** と入れます。

なお、COLUMNSの範囲は、A列でもC列でもX列でもどこでもいいです。

また、行も「1」でも「5」でも「100050」でもどこでもいいです。

ただここもROWS関数のところと同じですが注意することは、

① 「：」の前のセル番号には「$」を２つ（例では「$A$14」）、「：」の後のセル番号には「$」を後ろに一つ（例では「A$14」）付けること

② 「：」の前と後のセル番号は同じにすること（例では「：」の前も後も同じ「A14」）

の２つです。

すると下のようになります。

![8](https://user-images.githubusercontent.com/45871453/59075880-f3d65180-890d-11e9-98e7-ed587bab5231.jpg)

【入力した数式】

    =IFERROR(INDEX($A$3:$G$8,MATCH
    (LARGE(($F$3:$F$8="総務部")*1/ROW(
      $A$3:$A$8),ROWS($A$15:$A15)),1/ROW
      ($A$3:$A$8),0),COLUMNS($A$14:A$14)),"")

### 配列数式にする

数式はこれですべて入力できました。ただし、このままでは正しく動きません。

数式を｛ ｝が付く**「配列数式」** にする必要があるのです。

数式を配列数式にするには、数式を入力し終わった後、「Shift」キーと「Ctrl」キーを押しながら「Enter」キーを押す必要があります。

最後の仕上げにこれをやってください。

そうすると、｛｝が付いた次のような計算式が数式バーに表示されるはずです。


    {=IFERROR(INDEX($A$3:$G$8,MATCH(
      LARGE(($F$3:$F$8="総務部")*1/ROW($A$3:$A$8),
      ROWS($A$15:$A15)),1/ROW($A$3:$A$8),0),
      COLUMNS($A$14:A$14)),"")}


そして、この計算式を入れたセルには条件に当てはまった行の一番左上の値が表示されるはずです（例でいうと「総務部」という条件であれば「１（Ａ列の３行目の値）」）。

![9](https://user-images.githubusercontent.com/45871453/59075897-094b7b80-890e-11e9-97d0-362bb1f708bc.jpg)

### 他のセルに数式をコピーする

後はこの数式を、他のセルにコピーして貼り付けてあげる（セルA15をコピー→形式を選択して貼り付け→数式）と完了です。

例の完成形が下の図です。

![10](https://user-images.githubusercontent.com/45871453/59075906-19635b00-890e-11e9-8dc1-403a6f29e7f4.jpg)

以上です。
