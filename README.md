# start-git
A memo on how to link git and github. //gitとgithubの連携の方法のメモ書き

githubのアカウントページにて、<br>
Repositoriesタブから”New”をクリックする。<br>
<br>
“Public”を選び、<br>
“Add a README file”と“Choose a license “をチェックし、<br>
ライセンスはMIT Lisenceを選択する。<br>
“Create repository”をクリックすると、レポジトリの作成が完了する。<br>
<br>
--gitを初めて利用する場合-------------------------<br>
gitのバージョンを確認する
```
$ git --version
```
もし2.28よりも小さい場合、更新が必要。
```
$ sudo add-apt-repository ppa:git-core/ppa
$ sudo apt update
$ sudo apt upgrade
```

初期設定
```
git config --global user.name xxxxx(githubに登録した自分の名前)
git config --global user.email xxx@mail.address(githubに登録した自分のメールアドレス)
git config --global init.defaultbranch main
```

公開鍵をgithubに登録する
```
$ mkdir ~/.ssh
$ cd ~/.ssh
$ ssh-keygen -t rsa
$ cat id_rsa.pub
```

表示された文字列をすべてコピーする<br>
githubマイページの一番右上のアイコンから”Settings”をクリックする。<br>
左側のタブの”SSH and GPG keys”をクリックする。<br>
“New SSH key”をクリックする。<br>
“Title”にPCの名前を、”Key”にコピーした文字列を貼り付け、”Add SSH key”をクリックする。<br>
<br>
端末に戻り、
```
$ git config --global "url.git@github.com:.pushinsteadof" "https://github.com/"
```
--ここまで----------------------------------<br>
<br>
1.作成したレポジトリと同じ名前のフォルダを作成する。
```
$ mkdir ~/git/xxxxxx
$ cd ~/git/xxxxxx
```

2.初期化する
```
$ git init
```
3.githubのレポジトリと結びつける。
```
$ git remote add origin  https://github.com/username/repository.git
$ git pull origin main
```
“README.md”,”LICENSE”がフォルダ内に追加される<br>
<br>
4.作成したソースコードをフォルダ内に追加したら、
```
$ git add *
$ git commit -m “(Some commit message)”
$ git push origin main
```
githubのレポジトリにローカルのソースコードが反映される。<br>
<br>
ソースコードを更新したら4を繰り返す。<br>
<br>
##別のPCで作業をする場合
↑の１〜３を行う<br>
共有のPCの場合、初期設定は
```
$ cd ~/git/xxxxxx
$ git config --local user.name xxxxx(githubに登録した自分の名前)
$ git config --local user.email xxx@mail.address(githubに登録した自分のメールアドレス)
$ git config --local "url.git@github.com:.pushinsteadof" "https://github.com/"

```
とする<br>
秘密鍵の生成の際、パスワードを設定する。<br>

<br>
秘密鍵の名前がデフォルトだと、他人の操作によって上書きされる恐れがあるため、共有PCのときは名前を変更したほうがいいかもしれない。<br>
ただし、名前を変更した場合、そのままでは認識されないので、以下の処理を実行する。

```
$ cd ~/.ssh
$ touch config
$ vi config
Host github github.com
  HostName github.com
  IdentityFile ~/.ssh/（秘密鍵ファイル名）
  User git
```
