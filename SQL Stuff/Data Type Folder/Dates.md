| Data Type   | Description                                            |
| ----------- | ------------------------------------------------------ |
| `DATE`      | calendar date (year, month, day)                       |
| `TIME`      | time of day (hour, minute, second)                     |
| `TIMESTAMP` | date and time (year, month, day, hour, minute, second) |
https://www.postgresql.org/docs/current/datatype-datetime.html

Above is the different variations of timestamp

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    birth_date DATE,
    preferred_notification_time TIME,
    last_login TIMESTAMP
);

INSERT INTO users (id, birth_date, preferred_notification_time, last_login) VALUES
    (1, '1990-01-01', '12:00:00', '2024-01-01 12:00:00');
```

In the above example:

- `birth_date` is a `DATE` data type that stores the date of birth.
- `preferred_notification_time` is a `TIME` data type that stores the preferred time for notifications.
- `last_login` is a `TIMESTAMP` data type that stores the last login date and time
- 