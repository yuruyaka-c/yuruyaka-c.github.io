# Windows で C 言語を始める

このページでは、**Windows** に WSL2 と Ubuntu を用意し、Visual Studio Code で C 言語のプログラムを書いて実行する方法を説明します。

WSL2（Windows Subsystem for Linux 2）を使うと、Windows の中で Ubuntu を動かせます。この資料では、C 言語のコンパイルと実行は WSL2 上の Ubuntu で行います。

| デバイス | 対応状況 |
|--|:--:|
| Windows | ✅ |
| macOS |  |
| Ubuntu |  |
| iPad |  |
| Chrome OS |  |
| Android タブレット |  |

使うものは次の 3 つです。

| ソフトウェア | 用途 |
|---|---|
| WSL2 / Ubuntu | Windows 上で Ubuntu を動かす |
| GCC | C 言語のコードをコンパイルする |
| Visual Studio Code | C 言語のコードを書くエディタ |

## 1. WSL2 と Ubuntu をインストールする

この手順は、Windows 11 または Windows 10 バージョン 2004 以降を想定しています。

まず、PowerShell を管理者として開きます。

1. スタートメニューを開きます
2. `PowerShell` と入力します
3. **Windows PowerShell** または **ターミナル** を右クリックします
4. 「管理者として実行」を選びます

PowerShell で次のコマンドを実行します。

```powershell
wsl --install
```

インストールが終わったら、Windows を再起動します。

再起動後、Ubuntu の初期設定画面が表示されたら、画面の指示に従ってユーザー名とパスワードを設定します。

!!!info "パスワード入力について"
	Ubuntu のターミナルでは、パスワードを入力しても画面には文字が表示されません。何も入力されていないように見えても、実際には入力されています。入力後、++enter++ キーを押します。


## 2. WSL2 で動いているか確認する

PowerShell で次のコマンドを実行します。

```powershell
wsl -l -v
```

次のように、Ubuntu の `VERSION` が `2` になっていれば準備できています。

```txt
  NAME      STATE           VERSION
* Ubuntu    Running         2
```


## 3. Ubuntu を起動する

スタートメニューから **Ubuntu** を起動します。

以降、`sudo apt update` や `gcc -std=c2x hello.c` などの Linux 用コマンドは、Ubuntu のターミナルで実行します。


## 4. GCC をインストールする

C 言語のコードをコンパイルするために、`build-essential` というパッケージをインストールします。

Ubuntu のターミナルで次のコマンドを順に実行します。

```sh
sudo apt update
```

```sh
sudo apt install build-essential
```

途中で確認を求められたら、++y++ を入力して ++enter++ キーを押します。

`build-essential` をインストールすると、C 言語のコードをコンパイルするための `gcc`（ジーシーシー）というコマンドが使えるようになります。


## 5. gcc が使えるか確認する

Ubuntu のターミナルで次のコマンドを実行します。

```sh
gcc --version
```

次のように、バージョン情報が表示されれば準備完了です。

```txt
gcc (Ubuntu ...)
```

GCC 13 を使っている場合は、コンパイル時に `-std=c2x` を指定します。GCC 14 以降を使っている場合は、`-std=c23` を指定できます。


## 6. Visual Studio Code をインストールする

Visual Studio Code は、Windows 側にインストールします。

1. [Visual Studio Code :material-open-in-new:](https://code.visualstudio.com/){:target="_blank"} の公式サイトを開きます
2. Windows 版のインストーラーをダウンロードします
3. ダウンロードしたインストーラーを実行します
4. 画面の指示に従ってインストールします
5. Visual Studio Code を起動します


## 7. Visual Studio Code を日本語化する

Visual Studio Code は、インストール直後は英語のインターフェースになっていることがあります。次の手順で日本語化できます。

1. Visual Studio Code 左側の **Extensions** アイコンをクリックします
2. 検索欄に `Japanese Language Pack` と入力します
3. Microsoft の **Japanese Language Pack for Visual Studio Code** を選択します
4. **Install** を押します
5. 再起動を促すメッセージが表示されたら、Visual Studio Code を再起動します


## 8. WSL 拡張機能をインストールする

Visual Studio Code から WSL2 上の Ubuntu を扱えるようにするために、WSL 拡張機能をインストールします。

1. Visual Studio Code 左側の「拡張機能」アイコンをクリックします
2. 検索欄に `WSL` と入力します
3. Microsoft の **WSL** を選択します
4. 「インストール」を押します


## 9. C/C++ 拡張機能をインストールする

Visual Studio Code で C 言語のコードを扱いやすくするために、C/C++ 拡張機能をインストールします。

1. Visual Studio Code 左側の「拡張機能」アイコンをクリックします
2. 検索欄に `C/C++` と入力します
3. Microsoft の **C/C++** を選択します
4. 「インストール」を押します

WSL で開いたウィンドウでは、「WSL: Ubuntu にインストール」のようなボタンが表示されることがあります。その場合は、WSL 側にも C/C++ 拡張機能をインストールします。


## 10. 作業用フォルダを作る

C 言語のファイルを保存するためのフォルダを、WSL2 上の Ubuntu の中に作ります。

Ubuntu のターミナルで次のコマンドを実行します。

```sh
mkdir -p ~/c-practice
```

```sh
cd ~/c-practice
```

次のコマンドで、Visual Studio Code から `c-practice` フォルダを開きます。

```sh
code .
```

初回は、Visual Studio Code が WSL 用の準備を行うため、少し時間がかかることがあります。

Visual Studio Code の左下に `WSL: Ubuntu` のように表示されていれば、WSL2 上の Ubuntu に接続できています。

!!!info "ファイルを置く場所"
	WSL2 で C 言語を学習する場合は、`C:\Users\...` のような Windows 側のフォルダではなく、`~/c-practice` のような Ubuntu 側のフォルダにファイルを置くのがおすすめです。


## 11. 最初の C プログラムを書く

`c-practice` フォルダの中に、`hello.c` という名前のファイルを作成します。

`hello.c` に、次のコードを書いてみましょう。

```c title="hello.c"
#include <stdio.h>

int main()
{
	puts("Apple");
	puts("Banana");
}
```

このコードが、画面に `Apple` と `Banana` を表示するプログラムになります。


## 12. コンパイルして実行する

Visual Studio Code のメニューから「ターミナル」→「新しいターミナル」を選びます。

画面下にターミナルが表示されます。

左下に `WSL: Ubuntu` と表示されたウィンドウで開いたターミナルであれば、Ubuntu のターミナルとして使えます。

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


## 13. 入力を扱うプログラムを実行する

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

WSL2 上の Ubuntu では、実行中のプログラムに対してキーボードから直接入力できます。


## 14. よくあるトラブルと対処

!!! question "`wsl` が見つからない、または `wsl --install` が使えない"

	Windows のバージョンが古い可能性があります。

	Windows Update を実行してから、もう一度 `wsl --install` を試してください。

!!! question "Ubuntu のパスワードを入力しても画面に表示されない"

	Ubuntu のターミナルでは、パスワード入力中の文字は表示されません。

	何も入力されていないように見えても、実際には入力されています。パスワードを入力して ++enter++ キーを押してください。

!!! question "`gcc: command not found` と表示される"

	```txt title="エラーメッセージ"
	gcc: command not found
	```

	GCC がインストールされていない可能性があります。

	Ubuntu のターミナルで次のコマンドを実行します。

	```sh
	sudo apt update
	sudo apt install build-essential
	```

!!! question "`code: command not found` と表示される"

	```txt title="エラーメッセージ"
	code: command not found
	```

	Visual Studio Code が Windows 側にインストールされていないか、WSL から `code` コマンドを使う準備がまだできていない可能性があります。

	Windows 側で Visual Studio Code と WSL 拡張機能をインストールしてから、Ubuntu のターミナルを開き直してください。

!!! question "Visual Studio Code の左下に `WSL: Ubuntu` と表示されない"

	Windows 側のフォルダをそのまま開いている可能性があります。

	Ubuntu のターミナルで次のコマンドを実行して、WSL2 上のフォルダを Visual Studio Code で開きます。

	```sh
	cd ~/c-practice
	code .
	```

!!! question "`hello.c: No such file or directory` と表示される"

	```txt title="エラーメッセージ"
	cc1: fatal error: hello.c: No such file or directory
	compilation terminated.
	```

	ターミナルで開いているフォルダに `hello.c` がありません。

	Visual Studio Code で `hello.c` を保存したフォルダを開いているか確認してください。

!!! question "`a.out: command not found` と表示される"

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

!!! question "`invalid value 'c23' in '-std=c23'` と表示される"

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
