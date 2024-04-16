# Express.js × mysql × docker

参考: [Node.js+MySQL+Docker を使用した API の作成](https://qiita.com/t_k_t/items/93567a7ebe912da575c7)

## Error 対応

### 以下のコマンドで､ライブラリが入らない

```
npm install --save doting
```

代わりに`dotenv`を入れる

```
npm install dotenv
```

### mysql につながらない(500 Error)

```
Error: connect ECONNREFUSED 127.0.0.1:3306
backend-1  |     at PromisePool.execute (/usr/src/app/node_modules/mysql2/promise.js:374:22)
```

原因ソース

```ts
const dbConnect = mysql.createPool({
  host: process.env.DB_HOST,
  user: process.env.DB_USER,
  password: process.env.DB_PASSWORD,
  database: process.env.DB_NAME,
  connectTimeout: 100,
});
```

`.env`に各 key/value がセットされていない

```
DB_HOST="databaseホスト名"
DB_USER="user名"
DB_PASSWORD="パスワード"
DB_NAME="db名"
```

上記を追加し､`docker compose up`

参考 1: https://teratail.com/questions/302140

参考 2: https://www.npmjs.com/package/mysql2-promise
