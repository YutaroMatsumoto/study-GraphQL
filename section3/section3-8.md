# エイリアス（Aliass）

同じフィールドを並列で並べるのは文法上不正

```
// 間違い
user(login: "YutaroMatsumoto"){
    bio
    login
}
user(login: "a"){
  bio
  login
}

// 正しい
user1: user(login: "YutaroMatsumoto"){
    bio
    login
}
user2: user(login: "a"){
  bio
  login
}
```
