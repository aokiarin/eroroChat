eroroChat
===================


http://eelee.herokuapp.com/


ディレクトリ構成

    "# eroroChat" 
    .
    ├── chat.js
    ├── DB.sql
    ├── doc
    │   ├── command01.sh
    │   └── command02.sh
    ├── index.html
    ├── package.json
    ├── Procfile
    └── README.md



アプリ設定を表示  
`heroku config --app <アプリ名>`  
`heroku config --app secret-gorge-46628`  

MySQLのリモートホストに接続するコマンド  
`mysql -h <ホスト名> -u <ユーザ名> -p`  
`mysql -h us-cdbr-iron-east-03.cleardb.net -u bac9292c240c4a -p`  

sqlファイルを実行するコマンド  
`source <sqlファイルパス>`  
`source ./DB.sql`  

herokuのリモートレポジトリを追加するコマンド  
`heroku git:remote -a <herokuアプリ名>`  
`heroku git:remote -a secret-gorge-46628`  

ログをリアルタイムで表示  
`heroku logs --tail --app <herokuアプリ名>`  
`heroku logs --tail --app secret-gorge-46628`  




下記のように記述すればDB接続は可能だが、ハードコーディングは良くないし、
githubに公開する場合にセキュリティ的にだだ漏れ
//DBの設定
var db_config = {
    host:		'us-cdbr-iron-east-03.cleardb.net',
    user:		'bd61b3be7eaa27',
    password:	'fa04ea25',
    database:	'heroku_3f873eb64d6cbc6'
};
var connection = mysql.createConnection(db_config); 
    
環境変数を使えばDB情報ハードコードなしでいける  

`heroku config --app <アプリ名>`  

出力されたURLを以下で環境変数に登録

`heroku config:set DATABASE_URL="mysql2://<username>:<password>@<host>/<database>?reconnect=true&encoding=utf8mb4"  


あとは以下のようにコードから環境変数を使用してDBに接続する
`var connection = mysql.createConnection(process.env.DATABASE_URL);  


#Herokuログイン
heroku login

#プロジェクトのディレクトリに移動
#もうディレクトリ内なら不要
#cd <app-path>
#たとえば
#cd ~/work/chat

#gitを始めるコマンド
#git init

#全部のファイルをgitに認識させる（ステージに上げる）
git add .

#コミット
git commit -m "comment"

#herokuのリモートレポジトリを作成（アプリが作られる）
heroku create

#githubにプッシュ
git push origin master

#herokuへプッシュ（デプロイ）
git push heroku master
