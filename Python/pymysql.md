# pymysql

安装

`pip install pymysql`

使用

```python
import pymysql

user = 'root'
pwd = '123456'
dbname = 'mysql_test'
# 连接数据库
conn = pymysql.connect(host='localhost', user=user, password=pwd, database=dbname)
# 将返回值设置为字典，不填的话返回元组
cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
# 查询语句
select_student = 'select * from student;'
cursor.execute(select_student)
# 每获取一条指针就移动到下一个
result = cursor.fetchone()
print('result=', result)
result = cursor.fetchone()
print('result=', result)
result = cursor.fetchone()
print('result=', result)
# 如果要增、删、改数据，要commit
insert_student = 'insert into student (sname, gender, class_id) values (\'王巴\', \'男\', 2);'
cursor.execute(insert_student)
# 插入的最后一行ID
print('insert id=', cursor.lastrowid)
conn.commit()
# 查询所有
cursor.execute(select_student)
result = cursor.fetchall()
print('result=', result)
# 最后关闭
cursor.close()
conn.close()
```

