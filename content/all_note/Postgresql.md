
## Creating Database

```
CREATE DATABASE <database_name>;
```

## Creating Table

```
CREATE TABLE <table_name> (
    <column1> <datatype>,
    <column2> <datatype>,
    <column3> <datatype>
);
```

### DataTyps

1. Numeric Types

| Data Type         | Description            | Example   |
| ----------------- | ---------------------- | --------- |
| `INT` / `INTEGER` | Whole numbers          | 10, 25    |
| `BIGINT`          | Large numbers          | 999999999 |
| `DECIMAL(p,s)`    | Exact decimal numbers  | 10.50     |
| `NUMERIC`         | Same as DECIMAL        | 99.99     |
| `SERIAL`          | Auto-increment integer | 1, 2, 3   |

2. Character (Text) Types

|Data Type|Description|
|---|---|
|`VARCHAR(n)`|Limited text (max n characters)|
|`TEXT`|Unlimited text|
|`CHAR(n)`|Fixed-length text|

3. Date & Time Types ⏰