# Operation Name

無名の query は一つのリクエストで一つ。

```
以下のように書くことが可能
query getUser1 {
  useer1: user(login: "YutaroMatsumoto"){
    ...commonFields
  }

}

query getUser2 {
  useer1: user(login: "test"){
    ...commonFields
  }

}

fragment commonFields on User {
  bio
  login
}
```
