# 変数（Variables）

同じフィールドを並列で並べるのは文法上不正

```
// !は必須の意味
query ($login: String!) {
  user1: user(login: $login) {
    bio
    name
  }
}

// json
{
  "login": "YutaroMatsumoto"
}

```
