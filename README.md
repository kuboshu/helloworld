# Gitの練習のために"Hello World"と出力するだけのプログラムを投稿してみました

Gitの使い方習得のために、簡単なプログラムを作成して投稿してみました。
なお、以下の手順はカットアンドトライで実施していたので、内容に不正確の部分があるかもしれません。
内容に謝りがあったら都度修正しますので、ご指摘頂ければと思います

# 初めてのGitHub投稿 #

はじめてのGitHubへの投稿で少し手こずってしまったので、手順のメモを残しておきます。
なお、GitHubへの投稿は、PyCharmからEmacsを起動してmagitで実施しました。
PyCharmからEmacを起動する方法は
[PyCharmヘルプ](https://pleiades.io/help/pycharm/using-emacs-as-an-external-editor.html)
を参考にしました。

## GitHub上での作業 ##
まず、GitHubにアカウントを作成して、新しいリポジトリを作成します。

- GitHubにアカウントを作成する。
- レポジトリ"helloworld"を作成する。

## ローカルでの作業 ##
続いて、管理対象のフォルダを作成します。今回はPyCharmで作成したプロジェクト内のソースコードを管理しますので、
PyCharmでプロジェクトを作成してhelloworld.pyを作成します。

#### 1. PyCharmでプロジェクトを作成して、*helloworld.py*を作成する ####
PyCharmで"helloworld"というプロジェクトを作成して、Pythonのファイル*helloworld.py*を作成します。

#### 2. PyCharmのプロジェクトをGitの管理下におく ####
プロジェクトのディレクトリで以下のコマンドを実行して、プロジェクトのディレクトリをGitの管理下におきます。

```
$ git init
```

#### 3. ユーザー情報を登録します ####
Gitユーザの情報を登録します。以下の様にglobalのオプションをつけて登録すれば、
その後ローカルリポジトリを作成する度に実行する必要が無くなります。
なお、この作業はmagitでは無く、ターミナルから実行しています。
```
$ git config --global user.name ユーザー名
$ git config --global user.email ユーザーのメールアドレス
```

#### 4. プロジェクトをコミットする ####
プロジェクトの内容をコミットします。magitでのコミットに仕方はたくさんの記事があるので、そちらを参照してください。
また、このときGitの管理対象外にしたいファイルおよびディレクトリを*gitignore*に登録してください。

#### 5. リモートリポジトリを登録する ####
ローカルリポジトリを投稿するためのリモートリポジトリを登録します。
今回はGitHub上に作成した"helloworld"というリポジトリを登録します。
なお、この作業はmagitでは無く、ターミナルから実行しています。

```
git remote add origin https://github.com/kuboshu/helloworld.git
```

#### 6. リモートリポジトリとローカルリポジトリをマージする ####
リモートとローカルにそれぞれリポジトリを作成したので、この２つをマージしたいと思います。
今回はこのマージで手こずりました。
リモートレポジトリをローカルレポジトリにマージするには、リモートレポジトリの情報をローカルに取得(fetch)してから
内容をマージしますので、以下の様なコマンドをターミナル上で実行しました。

```
git fetch 
git merge origin/master
```

以下が実行結果で、マージができていないことがわかります。

```
$ git fetch
warning: no common commits
remote: Enumerating objects: 12, done.
remote: Counting objects: 100% (12/12), done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 12 (delta 1), reused 9 (delta 1), pack-reused 0
Unpacking objects: 100% (12/12), done.
From https://github.com/kuboshu/helloworld
 * [new branch]      master     -> origin/master
$ git merge origin/master
fatal: refusing to merge unrelated histories
```

ググった結果、 マージする際に以下の様にオプションをつけると解決するとあったので、


```
git merge --allow-unrelated-histories origin/master
```

オプションをつけたら以下の様に無事マージできました。

```
Merge made by the 'recursive' strategy.
 README.md     | 2 ++
 helloworld.py | 1 +
 2 files changed, 3 insertions(+)
 create mode 100644 README.md
 create mode 100644 helloworld.py
```


#### 7. ローカルリポジトリの更新をリモートリポジトリに反映させる #### 
リモートリポジトリをローカルリポジトリにマージしたので、それをリモートリポジトリにプッシュします。
これでローカルの内容がGitHubに反映されました。

```
git push origin master
```



