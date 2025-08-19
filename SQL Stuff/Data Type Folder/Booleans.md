Can only be true or false

```sql
CREATE TABLE users (
    is_active BOOLEAN
);

-- Insert true values --
INSERT INTO users (is_active) VALUES 
  (TRUE),
  (true),
  ('t'),
  ('y'),
  ('YES'),
  ('on'),
  ('1');

-- Insert false values --
INSERT INTO users (is_active) VALUES 
  (FALSE),
  (false),
  ('f'),
  ('N'),
  ('no'),
  ('OFF'),
  ('0');
```

Notice there there are many different ways to represent a boolean value in SQL

However for consistency, it is best to stick to a single representation of a boolean value in SQL