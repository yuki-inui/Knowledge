# Gitの操作方法

## ディレクトリ作成からファイルのupdateまで
.1 ディレクトリを作成し `git init` をやりリポジトリを作成する(ローカル)  　
.2 リポジトリ > ファイル　でファイルを作成する. 
.3 `git add ファイル` で変更情報を登録する(まだリポジトリに登録されてない). 　
.4 `git commmit -m "コメント"` をする. 
.5 `git log`で確認. 

.6 github でリポジトリを作成し　sshをおしてコピーをする　　
.7 `git remote add origin git@github.com:あなたのユーザー名/git-study.git
git branch -M main
git push -u origin main`　になる　　
.8 作成upload官僚　　

## 変更したい(ファイルの追加)とき
.1 ファイルを作成し前項の.3をからやる　　
.2 もし一括にファイルをアップロードしたかったら `git add .`をやる  それ以降順序通り　　
