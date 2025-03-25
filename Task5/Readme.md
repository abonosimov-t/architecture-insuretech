# Задание 5. Проектирование GraphQL API

## Схема GraphQL

```
type Query {
  client(id: String!): Client
  clientDocuments(id: String!): [Document]
  clientRelatives(id: String!): [Relative]
}

type Client {
  id: String
  name: String
  age: Int
}

type Document {
  id: String
  type: String
  number: String
  issueDate: String
  expiryDate: String
}

type Relative {
  id: String
  relationType: String
  name: String
  age: Int
}

```


## Запросы GraphQL
### Запрос пользователя

```
query GetClient($id: String!) {
  client(id: $id) {
    id
    name
    age
  }
}
```

### Запрос документов пользователя (eq `GET /clients/{id}`)

```
query GetClientDocuments($id: String!) {
  clientDocuments(id: $id) {
    id
    type
    number
    issueDate
    expiryDate
  }
}
```

### Запросы документов пользователя  (eq `GET /clients/{id}/documents`)

```
query GetClientDocuments($id: String!) {
  clientDocuments(id: $id) {
    id
    type
    number
    issueDate
    expiryDate
  }
}
```

### Запросы родственников пользователя  (eq `GET /clients/{id}/relatives`)

```
query GetClientRelatives($id: String!) {
  clientRelatives(id: $id) {
    id
    relationType
    name
    age
  }
}
```

### Все запросы в рамках одного запроса GraphQL

```
query GetClientFullInfo($id: String!) {
  client(id: $id) {
    id
    name
    age
  }
  clientDocuments(id: $id) {
    id
    type
    number
    issueDate
    expiryDate
  }
  clientRelatives(id: $id) {
    id
    relationType
    name
    age
  }
}
```