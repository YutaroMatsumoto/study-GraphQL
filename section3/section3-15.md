# ページネーション

## GraphQL のページネーション

relay style cursor pagination
1 件分のデータ：edge

client は適宜サーバーに対してデータの要求を行う
ある塊単位にデータを要求する

この塊：connection
connection が示す諸々の情報の集まりを Page と呼ぶ。
Page: edges + pageInfo(startCursor, endCursor, hasPreviousPage, hasNextPage)
startCursor：先頭の edge に含まれる cursor 情報
endCursor：最後尾の edge がもつ cursor 情報

## ユースケース

after の値：after で示す Cursor 情報よりも後ろのデータを要求するという意味を持つ？

- Request the First Page
  1 ページ目を取得する

  ```
  Request
  {
    query: "フロントエンドエンジニア",
    first: 5,
    after: null,
    last: null,
    before: null
  }

  Response
  {
    endCursor: "Y3Vyc29yOjU"
    hasNextPage: true
    hasPreviousPage: false
    startCursor: "Y3Vyc29yOjE="
  }

  ```

- Request the Next Page

```
  Request
  {
    query: "フロントエンドエンジニア",
    first: 5,
    after: "Y3Vyc29yOjU=",
    last: null,
    before: null
  }

  Response
  {
    endCursor: "Y3Vyc29yOjEw"
    hasNextPage: true
    hasPreviousPage: true
    startCursor: "Y3Vyc29yOjY="
  }
```

- Request the Previous Page

```
  Request
  {
    query: "フロントエンドエンジニア",
    first: null,
    after: null,
    last: 5,
    before: "Y3Vyc29yOjY="
  }

  Response
  {
    endCursor: "Y3Vyc29yOjU="
    hasNextPage: true
    hasPreviousPage: false
    startCursor: "Y3Vyc29yOjE="
  }
```

## GraphiQL で動かしてみる

```
query searchRepositories($first: Int, $after: String, $last: Int, $before: String, $query: String!) {
  search(first: $first, after: $after, last: $last, before: $before, query: $query, type: REPOSITORY) {
    repositoryCount
    pageInfo {
      endCursor
      hasNextPage
      hasPreviousPage
      startCursor
    }
    edges {
      cursor
      node {
        <!-- インラインフラグメントで取得 -->
        ... on Repository {
          id
          name
          url
        }
      }
    }
  }
}
```

### ※cursor について

base64 でエンコーディングされている文字列になる。<br>
各 edge に付与されている番号がエンコーディングされて、分かりづらい値になっている？

```
const cursors = ["Y3Vyc29yOjE=", "Y3Vyc29yOjI=", "Y3Vyc29yOjM=", "Y3Vyc29yOjQ="]
const results = corsors.map(cursor => {
  return new Buffer(cursor, 'base64').toString('binary')
})
```
