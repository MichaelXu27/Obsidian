There are several ways to store strings in PostgreSQL

| type         | description                                                    |
| ------------ | -------------------------------------------------------------- |
| `CHAR(n)`    | Fixed-length character string with a maximum length of `n`.    |
| `VARCHAR(n)` | Variable-length character string with a maximum length of `n`. |
| `TEXT`       | Variable-length character string without a maximum length.     |
It's preferred to use `TEXT` for strings since it can store a variable length of characters, `VARCHAR` is only good when you know the maximum length of the string you want to store

