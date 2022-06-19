# Fragments

```
// 以下のコードだとメンテナンス性が悪い
{
  user1: user(login: "YutaroMatsumoto"){
    bio
    login
  }
  user2: user(login: "a"){
    bio
    login
  }
}
```

```
以下のように書くことが可能
{
  useer1: user(login: "YutaroMatsumoto"){
    ...commonFields
  }

}

fragment commonFields on User {
  bio
  login
}
```

...fragment は、フラグメントスプレッドと呼ばれる
