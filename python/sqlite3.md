```python
import sqlite3 as db

connection = db.connect("my_database.sqlite")


orders = [
          ("A0002","2013-12-01","MSFT",1500,167.5),
          ("A0003","2013-12-02","GOOG",1500,167.5)
]
cursor.executemany("""INSERT INTO orders VALUES
    (?, ?, ?, ?, ?)""", orders)
connection.commit()

```

```python
stock = 'MSFT'
cursor.execute("""SELECT *
    FROM orders
    WHERE symbol=?
    ORDER BY quantity""", (stock,))
for row in cursor:
    print row
```
cursor.fetchone() 返回下一条内容， cursor.fetchall() 返回所有查询到的内容组成的列表（可能非常大）

```python
stock = 'AAPL'
cursor.execute("""SELECT *
    FROM orders
    WHERE symbol=?
    ORDER BY quantity""", (stock,))
cursor.fetchall()
```

关闭数据库

```python
cursor.close()
connection.close()
```    
