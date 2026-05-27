# Wandbox で C 言語を始める

このページでは、**Wandbox（ワンドボックス）**を使って C 言語のプログラムを実行する方法を説明します。Wandbox を使うと、パソコンやタブレットに開発環境をインストールせずに、Web ブラウザだけで C 言語のコードを試せます。

| デバイス | 対応状況 |
|--|:--:|
| Windows | ✅ |
| macOS | ✅ |
| Ubuntu | ✅ |
| iPad | ✅ |
| Chrome OS | ✅ |
| Android タブレット | ✅ |

## 1. Wandbox とは
Wandbox は、ユーザー登録なしで使えるオンラインコンパイラです。C 言語を含むさまざまなプログラミング言語で、コードのコンパイルと実行結果の確認ができます。パソコンやタブレットに何もインストールせずに、手軽に C 言語のプログラムを試したいときに便利です。

### 注意点
- 入力が必要なプログラムでは、実行前に「標準入力」欄へ入力内容を書きます
- 実行中にキーボードから対話的に入力することはできません
- ボランティアで運営されているサービスのため、アクセスが集中した際などに、コンパイルや実行に時間がかかることがあります

## 2. プログラムを書いて実行する

### 2.1 Wandbox を開く
1. [https://wandbox.org/ :material-open-in-new:](https://wandbox.org/){:target="_blank"} にアクセスします

### 2.2 設定を選ぶ
1. 画面左のメニューの**言語**で「C」を選択します
2. **コンパイラ**で「gcc 15」より新しいバージョンを選択します  
（下記の例では `gcc HEAD 17.0.0`）
3. **オプション**に「C11(GNU)」がある場合、「Compiler Default」に変更します
4. **コンパイル時オプション**欄は、最初は空欄のままでかまいません。  
第 10 章以降で数学関数を使う場合だけ `-lm` を入力します

![](../images/wandbox-1.png)

### 2.3 コードを書いて実行する
1. 画面の中央がエディタです。ここに C 言語のコードを書いていきます
2. エディタ上にコードを書いたら「実行」を押すとコンパイルが始まります
3. コンパイルが成功したら、そのプログラムが実行され、出力が表示されます

![](../images/wandbox-2.png)

```c title="実行するサンプルコード"
#include <stdio.h>

int main()
{
	puts("Apple");
	puts("Banana");
}
```
```txt title="実行結果"
Apple
Banana
```


## 3. 入力を扱うプログラムを実行する
- 第 3 章以降に出てくる `scanf()` のように、標準入力からの入力を扱うプログラムを実行する場合、あらかじめ右側の「標準入力」欄に入力内容を記述します
- 入力内容が複数ある場合、半角空白や改行で区切ります

![](../images/wandbox-3.png)

```c title="実行するサンプルコード"
#include <stdio.h>

int main()
{
	printf("商品の価格（円）を入力してください >\n");
	int price;
	scanf("%d", &price);

	printf("支払った金額（円）を入力してください >\n");
	int payment;
	scanf("%d", &payment);

	int change = payment - price;

	if (change < 0)
	{
		puts("支払金額が不足しています");
	}
	else
	{
		printf("おつり: %d 円\n", change);
	}
}
```
```txt title="標準入力欄の記入例"
880 1000
```
```txt title="実行結果"
商品の価格（円）を入力してください >
支払った金額（円）を入力してください >
おつり: 120 円
```


## 4. 書いたソースコードを他人と共有する
- 実行後に「:material-upload:共有」を押すと、書いた内容を URL で共有できます
	- URL の例: [https://wandbox.org/permlink/S8zs9kYzMAajKFUx](https://wandbox.org/permlink/S8zs9kYzMAajKFUx){:target="_blank"}
- URL は Web ブラウザの URL 欄からコピーします


## 5. Wandbox のよくあるトラブルとその対処

??? question "`cannot find -lm` と表示される"
	- [エラーの例 :material-open-in-new:](https://wandbox.org/permlink/T6uhQj4LAGd29o0N){:target="_blank"}

	```txt title="エラーメッセージ"
	/usr/bin/ld: cannot find -lm : No such file or directory
	collect2: error: ld returned 1 exit status
	```

	- 原因: Wandbox の「コンパイル時オプション」の欄に、不必要な空白文字が入っています。それがファイル名と解釈され、空白文字のファイルをコンパイルしようとしてエラーになっています
	- 解決法: 「コンパイル時オプション」の欄を空にします


??? question "`undefined reference to sqrt` と表示される"
	- [エラーの例 :material-open-in-new:](https://wandbox.org/permlink/mDiQJjcXtJIqoZcV){:target="_blank"}

	```txt title="エラーメッセージ"
	/usr/bin/ld: /tmp/ccUIxmmj.o: in function `main':
	prog.c:(.text+0x28): undefined reference to `sqrt'
	collect2: error: ld returned 1 exit status
	```

	- 原因: 数学関数を使うためのライブラリがリンクされていません（**第 10 章** 参照）
	- 解決法: Wandbox の[「コンパイル時オプション」欄に `-lm` を追加します :material-open-in-new:](https://wandbox.org/permlink/nNIIRLZYUYjZg5dW){:target="_blank"}
