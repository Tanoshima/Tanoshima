## staleTime cacheTime

- staleTime: キャッシュデータが古くなったとみなす時間
- cacheTime: データをキャッシュする時間

```
{
  staleTime: 0,
  cacheTime: 300000, (5m)
}

//5分以内にページ再読み込み => cacheのデータが表示 & バックグラウンドで再fetch
//5分以降にページ再読み込み => 再fetch
```
