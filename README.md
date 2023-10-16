### How to run local server

```
supabase start
pnpm i
pnpm run dev
```

### stop local db

```
supabase stop

```

###　 db migration(基本的にローカルで)

```
$ npx prisma migrate dev --name init
$ npx prisma generate
```

> prisma を使う場合は env を本番用と開発用で分けてください。

## prisma を使わない場合以下

### サーバーとリモートを接続

> https://supabase.com/dashboard/project/[project-id]

```
supabase login(https://supabase.com/dashboard/account/tokensで作成)
supabase link --project-ref [project-id] --password [Database Password]

```

### サーバーとローカルの migration を比較同期

> supabase 管理画面で追加した table を追加したい場合

```
supabase db diff --file [migrate-file-name]
```

```
supabase migration list (違いを判別)
```

> 上記で違いがある場合
> case: サーバー側のスキーマをローカルに反映

```
supabase db pull
```

> case: ローカルのスキーマをサーバーに反映

```
supabase db pull
```

> ３つのコマンドを実行すると、スキーマに違いはなくなります

```
supabase db reset
supabase db push
supabase db pull
```

### 簡素なトラブルシューティング

> ローカルの Supabase ダッシュボードからテーブルをいじったり、
> SQL 文や Seed ファイルにデータをいろいろ触ったら supabase db reset して整合性をとってください。
> また、マイグレーションファイルを削除したら、削除した部分のスキーマを Supabase の DB から消すことも出来ます。
> エラーが出たら、supabase コマンドで docker を再起動してみてください

```
supabase stop
supabase start
```

> 開発用 本番用 db は env で切り替えれますが基本的には開発用で運用してください
