mysql

### rollback和start transaction不能同时用一个execute执行

```python
def start_transaction(db=None):
    try:
        cursor = db.cursor()
        SQL = "start transaction;"
        cursor.execute(SQL)
        print("start transaction")
    except Exception:
        print("start transaction fail")
    cursor.close()


def rollback(db=None):
    try:
        cursor = db.cursor()
        SQL = """rollback;"""
        cursor.execute(SQL)
    except Exception:
        print("rollback fail")
    cursor.close()
```

```python
get_characteristic
```

这个函数没有用validation来判断

```python
get_characteristic_unity_and_value
```

这个用validation来判断

SELECT * FROM attribute as a
WHERE
a.attribute = '**Aspirine**' and a.unity = '%' and a.`value` = 5

Aspirine必须要加''

### 创建临时表

with element_to_be_deleted as(select DISTINCT a.id
FROM
attribute as a
where
a.id not in (
select DISTINCT b.id_attribute
FROM
attribute_coating as b)
)

select * from element_to_be_deleted

### 删除表时遇到specify

https://stackoverflow.com/questions/5816840/delete-i-cant-specify-target-table/41752499