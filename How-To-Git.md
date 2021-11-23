# Gitの操作方法

## ディレクトリ作成からファイルのupdateまで
1. ディレクトリを作成し `git init` をやりリポジトリを作成する(ローカル)
2. リポジトリ > ファイル　でファイルを作成する
3. `git add ファイル` で変更情報を登録する(まだリポジトリに登録されてない)　
4. `git commmit -m "コメント"` をする
5. `git log`で確認.<br><br>  以下リモートリポジトリ  
 
7. github でリポジトリを作成し　sshをおしてコピーをする　`or push an existing...`　
8. `git remote add origin git@github.com:あなたのユーザー名/git-study.git
git branch -M main
git push -u origin main`　を実行
8. 作成upload完了

## 変更したい(ファイルの追加)とき
1. ファイル作成し前項の3. から進める　　
2. 全部のファイルを上げたい時は `git add .`をやる  それ以降　
