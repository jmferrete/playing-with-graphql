
# More examples

Some example queries to execute into http://graphql-swapi.parseapp.com/ online app.

## Retrieve all types

```graphql
{
  __schema {
    types {
      name
      kind
      description
    }
  }
}
```

## All types with their fields

```graphql
{
	__schema {
    types {
      name
      kind
      fields {
        name
      }
    }
  }
}
```

## All people

```graphql
{
  allPeople {
    edges {
      node {
        id
        name
      }
    }
  }
}
```

## All people with the films

```graphql
{
  allPeople {
    edges {
      node {
        id
        name
        filmConnection {
          edges {
            node {
              title
            }
          }
        }
      }
    }
  }
}
```

## All people with the films and their starships

```graphql
{
  allPeople {
    edges {
      node {
        id
        name
        filmConnection {
          edges {
            node {
              title
              starshipConnection {
                edges {
                  node {
                    name
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
```

## The name of an specific person

```graphql
{
  # Luke Skywalker ID
  person(id: "cGVvcGxlOjE=") {
    name
  }
}
```

## The name of an specific person with an alias

```graphql
{
  # Luke Skywalker ID
  luke: person(id: "cGVvcGxlOjE=") {
    name
  }
}
```

## The name of an specific person with an alias

```graphql
{
  luke: person(id: "cGVvcGxlOjE=") {
    name
  }
  obi_wan: person(id: "cGVvcGxlOjEw") {
    name
  }
}
```

## The name and starships of two persons using a fragment

```graphql
{
  luke: person(id: "cGVvcGxlOjE=") {
    ...comparisonFields
  }
  obi_wan: person(id: "cGVvcGxlOjEw") {
    ...comparisonFields
  }
}

fragment comparisonFields on Person {
  name
  starshipConnection {
    edges {
      node {
        name
      }
    }
  }
}
```

## Now using a variable

```graphql
query personName($id: ID) {
  person(id: $id) {
    name
  }
}
```

Variables:
```json
{
  "id": "cGVvcGxlOjE="
}
```

## Directives

```graphql
query personName($id: ID, $withStarships: Boolean!) {
  person(id: $id) {
    name
    starshipConnection @include(if: $withStarships) {
      edges {
        node {
          name
        }
      }
    }
  }
}
```

Variables:
```json
{
  "id": "cGVvcGxlOjE=",
  "withStarships": true
}
```
