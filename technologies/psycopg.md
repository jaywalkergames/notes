A Postgres database adapter for Python.
# Overview
### Use
```python
import psycopg2

# Connect to your postgres DB
conn = psycopg2.connect("dbname=test user=postgres")

# Open a cursor to perform database operations
with conn.cursor() as cursor:
    cursor.execute("SELECT * FROM my_data")

# Retrieve query results
records = cur.fetchall()

conn.close()
```
### Installation
`pip install psycopg2-binary`
# Technical
### Connection Class
Handles connection to a Postgres database.
Thread safe and can be shared among many threads.
Psycopg2 guarantees a reliable and uninterrupted data transfer channel, enhancing the efficiency of data exchange and communication.
### Cursor Class
Allows Python code to execute PostgreSQL command in a database session.
Cursors are _not_ thread safe: a multithread application can create many cursors from the same connection and should use each cursor from a single thread.
- Psycopg2 is equipped with capabilities for precise and rapid SQL query execution.
- The cursor ensures data is up to date in real-time in each thread.
### from psycopg2 import sql
```python
# Template variables
query = sql.SQL("select {field} from {table} where {pkey} = %s").format(
    field=sql.Identifier('my_name'),
    table=sql.Identifier('some_table'),
    pkey=sql.Identifier('id'))

# For list of fields
query = sql.SQL("select {fields} from {table}").format(
    fields=sql.SQL(',').join([
        sql.Identifier('field1'),
        sql.Identifier('field2'),
        sql.Identifier('field3'),
    ]),
    table=sql.Identifier('some_table'))
```
### Python to SQL Types
| Python                                                                                                                                                                                                                                                                                                                                | PostgreSQL                                  | See also                                                                                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `None`                                                                                                                                                                                                                                                                                                                                | `NULL`                                      | [Constants adaptation](https://www.psycopg.org/docs/usage.html#adapt-consts)                                                                                        |
| `bool`                                                                                                                                                                                                                                                                                                                                | `bool`                                      |                                                                                                                                                                     |
| `float`                                                                                                                                                                                                                                                                                                                               | `real`<br><br>`double`                      | [Numbers adaptation](https://www.psycopg.org/docs/usage.html#adapt-numbers)                                                                                         |
| `int`<br><br>`long`                                                                                                                                                                                                                                                                                                                   | `smallint`<br><br>`integer`<br><br>`bigint` |                                                                                                                                                                     |
| [`Decimal`](https://docs.python.org/3/library/decimal.html#decimal.Decimal "(in Python v3.13)")                                                                                                                                                                                                                                       | `numeric`                                   |                                                                                                                                                                     |
| `str`<br><br>`unicode`                                                                                                                                                                                                                                                                                                                | `varchar`<br><br>`text`                     | [Strings adaptation](https://www.psycopg.org/docs/usage.html#adapt-string)                                                                                          |
| `buffer`<br><br>[`memoryview`](https://docs.python.org/3/library/stdtypes.html#memoryview "(in Python v3.13)")<br><br>[`bytearray`](https://docs.python.org/3/library/stdtypes.html#bytearray "(in Python v3.13)")<br><br>[`bytes`](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.13)")<br><br>Buffer protocol | `bytea`                                     | [Binary adaptation](https://www.psycopg.org/docs/usage.html#adapt-binary)                                                                                           |
| `date`                                                                                                                                                                                                                                                                                                                                | `date`                                      | [Date/Time objects adaptation](https://www.psycopg.org/docs/usage.html#adapt-date)                                                                                  |
| `time`                                                                                                                                                                                                                                                                                                                                | `time`<br><br>`timetz`                      |                                                                                                                                                                     |
| `datetime`                                                                                                                                                                                                                                                                                                                            | `timestamp`<br><br>`timestamptz`            |                                                                                                                                                                     |
| `timedelta`                                                                                                                                                                                                                                                                                                                           | `interval`                                  |                                                                                                                                                                     |
| `list`                                                                                                                                                                                                                                                                                                                                | `ARRAY`                                     | [Lists adaptation](https://www.psycopg.org/docs/usage.html#adapt-list)                                                                                              |
| `tuple`<br><br>`namedtuple`                                                                                                                                                                                                                                                                                                           | Composite types<br><br>`IN` syntax          | [Tuples adaptation](https://www.psycopg.org/docs/usage.html#adapt-tuple)<br><br>[Composite types casting](https://www.psycopg.org/docs/extras.html#adapt-composite) |
| `dict`                                                                                                                                                                                                                                                                                                                                | `hstore`                                    | [Hstore data type](https://www.psycopg.org/docs/extras.html#adapt-hstore)                                                                                           |
| Psycopg’s `Range`                                                                                                                                                                                                                                                                                                                     | `range`                                     | [Range data types](https://www.psycopg.org/docs/extras.html#adapt-range)                                                                                            |
| Anything™                                                                                                                                                                                                                                                                                                                             | `json`                                      | [JSON adaptation](https://www.psycopg.org/docs/extras.html#adapt-json)                                                                                              |
| [`UUID`](https://docs.python.org/3/library/uuid.html#uuid.UUID "(in Python v3.13)")                                                                                                                                                                                                                                                   | `uuid`                                      | [UUID data type](https://www.psycopg.org/docs/extras.html#adapt-uuid)                                                                                               |
| [`ipaddress`](https://docs.python.org/3/library/ipaddress.html#module-ipaddress "(in Python v3.13)") objects                                                                                                                                                                                                                          | `inet`<br><br>`cidr`                        | [Networking data types](https://www.psycopg.org/docs/extras.html#adapt-network)                                                                                     |
