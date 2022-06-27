# インラインフラグメント（Inline Fragments）と型名（\_\_typename）

```
query search {
  search(query: "We work hard", type: USER, first: 2) {
    nodes {
			#Userの方の中のid, name, urlフィールドをnodes直下に展開
      ... on User {
        id
        name
        url
      }
      ... on Organization {
        id
        name
        url
        projectsUrl
      }
    }
  }
}
```

```
<!-- 以下の記述だとフィールドの構造が同じのため、どのnodeがどういった型のデータかが判別できなくなる。 -->
<!-- 何の型なのかも返してもらいたいときに__typenameを利用する -->
query search {
  search(query: "We work hard", type: USER, first: 2) {
    nodes {
			#Userの方の中のid, name, urlフィールドをnodes直下に展開
      ... on User {
        id
        name
        url
      }
      ... on Organization {
        id
        name
        url
      }
    }
  }
}
```

```
<!--  __typenameを利用した場合 -->
query searchWithTypeName {
  search(query: "We work hard", type: USER, first: 2) {
    nodes {
      __typename
      ... on User {
        id
        name
        url
      }
      ... on Organization {
        id
        name
        url
        projectsUrl
      }
    }
  }
}
```
