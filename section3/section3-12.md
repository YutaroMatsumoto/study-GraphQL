# ミューテーション（Mutations）

データの更新・削除には Mutation という機能を使う必要がある。
実際のアプリケーションでは頻繁に利用する

```
<!-- repository情報の取得 -->
query getRepository {
  repository(owner: "YutaroMatsumoto", name: "study-GraphQL") {
    id
    name
    url
  }
}
```

```
<!-- addStar -->
mutation addStar{
  addStar(input: {
    starrableId: "R_kgDOHe89Rw",
  }) {
    starrable{
      id
      viewerHasStarred
    }
  }
}
```

```
<!-- removeStar -->
mutation removeStar {
  removeStar(input: {
    starrableId: "R_kgDOHe89Rw",
  }) {
    starrable{
      id
      viewerHasStarred
    }
  }
}
```
