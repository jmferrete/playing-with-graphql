# Graphene-django example

Basic Django app based in graphene-django cookbook example app (https://github.com/graphql-python/graphene-django/tree/master/examples/cookbook)

# Some example queries

## See all schema types
### Query
```graphql
{
    __schema {
        types {
            name
        }
    }
}
```

## See all objects of type ingredient
```graphql
{
    allIngredients {
        edges {
            node {
                id
                name
            }
        }
    }
}
```


## A simple query with one operation
### Query
```graphql
ingredient(id:"SW5ncmVkaWVudE5vZGU6MQ==") {
    name
    notes
}
```

## Two operations with variables (operationName must be expecified)
### Query
```graphql
query getIngredientName($identifier: ID!) {
    ingredient(id:$identifier) {
        name
    }
}

query getIngredientNotes($identifier: ID!) {
    ingredient(id:$identifier) {
        notes
    }
}
```
### Variables
```json
{
    "identifier": "SW5ncmVkaWVudE5vZGU6MQ=="
}
```

