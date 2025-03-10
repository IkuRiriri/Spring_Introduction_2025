# For Windows Users
以下の事前準備をお願いします．
- [ ] WSL2の準備
- [ ] Githubアカウントの作成
- [ ] Githubアカウントとwsl2のSSH接続
- [ ] Docker Desktopのインストール
- [ ] VSCodeの設定 

## WSL2の準備
WSL2（Windows Subsystem For Linux）は，Windows上でLinuxを動かすことのできるソフトウェアです．本講習では，WSL2の利用を前提としています．
まず，Microsoft Store から，Windows Terminal をダウンロードしてください．

![Windows Terminal](./figures/windows_terminal.png "Windows Terminal")

続いて，Microsoft Storeで Ubuntu をダウンロードしてください．もし，すでに WSL2 で Ubuntu を使用しているという場合は，Ubuntu 24.04.1 LTS を使用しても構いません．

![Ubuntu List](./figures/ubuntu_list.png "Ubuntu List")

インストール後， "開く" を押下します．

![Ubuntu Open](./figures/ubuntu_dl.png "Ubuntu Open")

起動後，ターミナルが開き，Ubuntu が起動します．数分間の待機後，Username と Password の設定を求められます．

~~~bash
Enter new UNIX username:
New password:
~~~

パスワードの設定後，以下の表示が確認でき，入力を受け付けるようになれば完了です．

~~~bash
username@DESKTOP-id:~$
~~~

以下のコマンドを実行して，Ubuntu をアップデートしておきましょう．
~~~bash
$ sudo apt update
$ sudo apt dist-upgrade
~~~

## Github アカウントの作成
git は，ソースコードのバージョン管理ソフトウェアであり，ソースコードの変更履歴を残すことができます．また，Github を使用することで，自分のソースコードを他のユーザと共有したり，共同で同じソースコードを修正したりすることができます．研究において作成したソースコードは，全てバージョン管理を行うことを強く推奨します．

[Github のホームページ](https://github.co.jp/ "Github のホームページ")の右上にある Sign up を押下し，アカウントを作成してください．すでにアカウントを所持している場合は必要ありません．使用するメールアドレスは自由ですが，大学のメールアドレス（ドメインが`??.ritsumei.ac.jp`）を使用すると学生の認証ができ，有料機能の一部を無料で使用することができます．

Github アカウントを確認するために，[本レポジトリのアカウント登録用ページ](https://github.com/IkuRiriri/Spring_Introduction_2025/issues/1 "本レポジトリのアカウント登録用ページ")に飛び，指示の通りの登録をお願いします．なお，使用したメールアドレスが大学のもの（ドメインが`??.ritsumei.ac.jp`），もしくは研究室のもの（`name.aislab@gmail.com`）である場合はメールアドレスのみで十分です．

## Githubアカウントとwsl2のSSH接続

先程セットアップした Ubuntu と，Github アカウントで SSH 接続を行います．SSH とは，Secure SHell の略称で，これを使用することで暗号化された安全な通信を行うことができます．今回は，公開鍵暗号を使用します．
なお，既にアカウントを SSH 接続している場合は必要ありません．

始めに，Ubuntu 上の git に対し，username と メールアドレスの設定を行います．Github アカウントと同じものを使用することを推奨します．

~~~bash
$ git config --global user.name [任意のusername]
$ git config --global user.email [任意のメールアドレス]
~~~

続いて，公開鍵暗号を作成します．一般的に ssh 鍵は，ホームディレクトリ直下に保管することが慣習であるため，本講習においてもそれに習います．秘密鍵に対するパスワードの設定を求められるため，設定してください．

~~~bash
$ ssh-keygen -t ed25519 -C "[任意のメールアドレス]" -f ~/.ssh/github
~~~

次に，公開鍵を Github アカウントへと登録します．以下のコマンドで出力される公開鍵をコピーします．

~~~bash
$ cat ~/.ssh/github.pub
~~~
ログインした状態で[Github のホームページ](https://github.com/ "Github のホームページ")にアクセスし，右上のユーザアイコンを押下し，Settings > SSH and GPG keys > New SSH key を選択します．

Title に接続先の識別名（ex: Ubuntu），Key に先ほどコピーした公開鍵を入力し，Add SSH key で登録します．

![ssh4](./figures/ssh4.png "ssh4")

これで，Githubアカウントに対して公開鍵が設定されました．
正しく設定できていることを確認するために，接続テストを行います．

Ubuntu のターミナルで以下のコマンドを実行します．秘密鍵のパスワードを求められた場合は，設定したパスワードを入力してください．

~~~bash
$ ssh -T git@github.com
~~~

Githubアカウントのユーザ名が確認できたら成功です．

<details><summary>うまくいかない場合</summary>

`~/.ssh/config`に以下のファイルを追加してみてください．
~~~
Host github github.com
  HostName github.com
  IdentityFile ~/.ssh/github
  User git
~~~
</details>

## Docker Desktop のインストール
[docker](https://docs.docker.com/desktop/setup/install/windows-install/ "docker")のページの指示に従って，Docker Desktopをインストールしてください．

インストール時に，`Use WSL 2 instead of Hyper-V (recommended)`にチェックが付いていることを確認してください．

![DockerDesktopInstall](./figures/dockerdesktop_wsl.png "DockerDesktopInstall")

その後，PC 本体の再起動を行い，Docker Desktopが起動すれば成功です．
アカウントの登録に関しては，今回の講習では必要ありませんので，登録したい方のみで大丈夫です．

確認のために，WSL2 上の Ubuntu で以下のコマンドを実行してみましょう．

~~~bash
$ docker --version
Docker version xx.x.x
~~~

Docker のバージョンが表示されれば，成功です．

## VSCode のインストール
[VSCode](https://code.visualstudio.com/download "VSCode") のホームページから VSCode をインストールしてください．

また，以下の拡張機能を使用するので，併せてダウンロードしてください．
- [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)
- [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
- [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop)

以上で事前準備は終了です．