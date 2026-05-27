# Ubuntu で C 言語を始める

このページでは、**Ubuntu** に C 言語の開発環境を用意し、Visual Studio Code で C 言語のプログラムを書いて実行する方法を説明します。

| デバイス | 対応状況 |
|--|:--:|
| Windows |  |
| macOS |  |
| Ubuntu | ✅ |
| iPad |  |
| Chrome OS |  |
| Android タブレット |  |

使うものは次の 2 つです。

| ソフトウェア | 用途 |
|---|---|
| GCC | C 言語のコードをコンパイルする |
| Visual Studio Code | C 言語のコードを書くエディタ |

## 1. ターミナルを開く

Ubuntu では、ターミナルからコマンドを実行して、必要なソフトウェアをインストールします。

ターミナルは次のどちらかの方法で開けます。

- ++ctrl+alt+t++ を押します
- 画面左下のアプリ一覧から「端末」または「Terminal」を起動します


## 2. GCC をインストールする

C 言語のコードをコンパイルするために、`build-essential` というパッケージをインストールします。

ターミナルで次のコマンドを順に実行します。

```sh
sudo apt update
```

```sh
sudo apt install build-essential
```

途中で確認を求められたら、++y++ を入力して ++enter++ キーを押します。

`build-essential` をインストールすると、C 言語のコードをコンパイルするための `gcc`（ジーシーシー）というコマンドが使えるようになります。


## 3. gcc が使えるか確認する

ターミナルで次のコマンドを実行します。

```sh
gcc --version
```

次のように、バージョン情報が表示されれば準備完了です。

```txt
gcc (Ubuntu ...)
```

GCC 13 を使っている場合は、コンパイル時に `-std=c2x` を指定します。GCC 14 以降を使っている場合は、`-std=c23` を指定できます。


## 4. Visual Studio Code をインストールする

Visual Studio Code は、Microsoft 公式サイトから `.deb` パッケージをダウンロードしてインストールします。

Ubuntu Software や App Center からインストールする方法もありますが、Snap 版がインストールされることがあります。この資料では、C 言語の開発環境として使いやすいように、公式 `.deb` 版を使います。

1. [Visual Studio Code :material-open-in-new:](https://code.visualstudio.com/){:target="_blank"} の公式サイトを開きます
2. Linux 用の `.deb` ファイルをダウンロードします
3. ダウンロードしたファイルがあるフォルダを開きます
4. フォルダ内の何もない場所を右クリックし、「端末で開く」を選びます
5. 次のコマンドを実行します

```sh
sudo apt install ./code_*.deb
```

途中で確認を求められたら、++y++ を入力して ++enter++ キーを押します。

インストール後、アプリ一覧から Visual Studio Code を起動します。

`.deb` 版のインストール中に、Visual Studio Code の更新用リポジトリを登録するか確認されることがあります。登録すると、以降は Ubuntu の通常のアップデートと一緒に更新できます。


## 5. Visual Studio Code を日本語化する

Visual Studio Code は、インストール直後は英語のインターフェースになっていることがあります。次の手順で日本語化できます。

1. Visual Studio Code 左側の **Extensions** アイコン :material-view-grid-outline: をクリックします
2. 検索欄に `Japanese Language Pack` と入力します
3. Microsoft の **Japanese Language Pack for Visual Studio Code** を選択します
4. **Install** を押します
5. 再起動を促すメッセージが表示されたら、Visual Studio Code を再起動します


## 6. C/C++ 拡張機能をインストールする

Visual Studio Code で C 言語のコードを扱いやすくするために、C/C++ 拡張機能をインストールします。

1. Visual Studio Code 左側の「拡張機能」アイコン :material-view-grid-outline: をクリックします
2. 検索欄に `C/C++` と入力します
3. Microsoft の **C/C++** を選択します
4. 「インストール」を押します


## 7. 作業用フォルダを作る

C 言語のファイルを保存するためのフォルダを作ります。

例えば、ホームフォルダの「ドキュメント」の中に、次のようなフォルダを作ります。

```txt
ドキュメント
└── c-practice
```

Visual Studio Code で、この `c-practice` フォルダを開きます。

1. Visual Studio Code を開きます
2. 「ファイル」→「フォルダーを開く...」を選びます
3. 作成した `c-practice` フォルダを選びます
4. フォルダを信頼するか確認された場合は、内容を確認してから「はい、作成者を信頼します」を選びます


## 8. 最初の C プログラムを書く

`c-practice` フォルダの中に、`hello.c` という名前のファイルを作成します。

`hello.c` に、次のコードを書いて保存します。

```c title="hello.c"
#include <stdio.h>

int main()
{
	puts("Apple");
	puts("Banana");
}
```

このコードが、画面に `Apple` と `Banana` を表示するプログラムになります。


## 9. コンパイルして実行する

Visual Studio Code のメニューから「表示」→「ターミナル」を選びます。

画面下にターミナルが表示されます。

次のコマンドを入力して、プログラムをコンパイルします。

```sh
gcc -std=c2x hello.c
```

コンパイルに成功すると、`a.out` という実行ファイルが作られます。エクスプローラー上でも `a.out` を確認できます。

次のコマンドで実行します。

```sh
./a.out
```

ターミナル内に次のように表示されれば成功です。

```txt title="出力"
Apple
Banana
```


## 10. 入力を扱うプログラムを実行する

次のプログラムは、商品の価格と支払金額を入力し、おつりを計算します。

`hello.c` の内容を次のコードに書き換えて保存します。

```c title="hello.c"
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

コンパイルします。

```sh
gcc -std=c2x hello.c
```

実行します。

```sh
./a.out
```

実行中に入力を求められたら、数字を入力して Enter キーを押します。

```txt title="入力例"
商品の価格（円）を入力してください >
880
支払った金額（円）を入力してください >
1000
おつり: 120 円
```

Ubuntu のターミナルでは、実行中のプログラムに対してキーボードから直接入力できます。


## 11. おすすめのコンパイルコマンド

コンパイラ・オプションの意味は [**付録 3. コンパイラ・オプション**](../appendix/compiler-options.md) を参照してください。

=== "GCC 14 以降"
	```txt title="コンパイルコマンド"
	gcc -Wall -Wextra -Wvla -Wstrict-prototypes -Wconversion -Wshadow -pedantic -std=c23 hello.c -lm
	```

=== "GCC 13"
	```txt title="コンパイルコマンド"
	gcc -Wall -Wextra -Wvla -Wstrict-prototypes -Wconversion -Wshadow -pedantic -std=c2x hello.c -lm
	```


## 12. よくあるトラブルと対処

??? question "`gcc: command not found` と表示される"

	```txt title="エラーメッセージ"
	gcc: command not found
	```

	GCC がインストールされていない可能性があります。

	次のコマンドを実行します。

	```sh
	sudo apt update
	sudo apt install build-essential
	```

??? question "`hello.c: No such file or directory` と表示される"

	```txt title="エラーメッセージ"
	cc1: fatal error: hello.c: No such file or directory
	compilation terminated.
	```

	ターミナルで開いているフォルダに `hello.c` がありません。

	Visual Studio Code で `hello.c` を保存したフォルダを開いているか確認してください。

??? question "`a.out: command not found` と表示される"

	```txt title="エラーメッセージ"
	a.out: command not found
	```

	実行するときは、ファイル名の前に `./` を付けます。

	```sh title="誤った実行方法"
	a.out
	```

	```sh title="正しい実行方法"
	./a.out
	```

??? question "`invalid value 'c23' in '-std=c23'` と表示される"

	```txt title="エラーメッセージ"
	gcc: error: unrecognized command-line option '-std=c23'
	```

	使用している GCC が `-std=c23` に対応していない可能性があります。

	次のコマンドでバージョンを確認します。

	```sh
	gcc --version
	```

	GCC 13 を使っている場合は、`-std=c23` の代わりに `-std=c2x` を指定します。

	```sh
	gcc -std=c2x hello.c
	```
