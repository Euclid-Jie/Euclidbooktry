先占坑，以后填

## Python 连接

```python
from clickhouse_driver import Client

# Connect to ClickHouse
client = Client(host='localhost', port=9000, user='default', password='123456')

# Create a table if it doesn't exist
client.execute('CREATE TABLE IF NOT EXISTS my_table (id Int32, name String) ENGINE = MergeTree() ORDER BY id')

# Insert data into the table
data = [(1, 'John'), (2, 'Jane'), (3, 'Alice')]
client.execute('INSERT INTO my_table (id, name) VALUES', data)
```

