# Exposed

https://github.com/JetBrains/Exposed

## How do I create relations between objects/tables?

- ???

## How do I query children of a given object?

i.e Get all Transactions of Type "income"

- ???

## How do I create a new entry in the DB with multiple values

```
TransactionDAO.new {
  amount = body.amount
  type = body.type.toString()
}
```

## How do I create a new DB migration?

Use a tool like [FlyWay](https://flywaydb.org)
