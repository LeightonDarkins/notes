# FlyWay

Database Migrations

https://flywaydb.org

---

## How do I create a new table with FlyWay?

- add `compile "org.flywaydb:flyway-core:4.1.1"` to gradle dependencies
- create a new directory `src/main/resources/db/migration`
- create a new migration file `V1_0_0__CreateTransactionsTable.sql`
- add whatever SQL needs to run

```
CREATE TABLE transactions (
    id UUID NOT NULL,
    amount BIGINT NOT NULL,
    type VARCHAR(50) NOT NULL
);
```

- place this code somewhere around application startup

```
val flyway = Flyway()
flyway.setDataSource(*dbUrl*, *dbUsername*, *dbPassword*)
flyway.migrate()
```

- run the application

## How do I change a table with FlyWay?

- create a new migration file `V1_0_1__AddDateToTransactionTable.sql`
- add whatever SQL needs to run

```
ALTER TABLE transactions ADD date DATE;
```

- run the application
