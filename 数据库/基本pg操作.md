https://www.ruanyifeng.com/blog/2013/12/getting_started_with_postgresql.html#:~:text=%E7%AC%AC%E4%B8%80%E7%A7%8D%E6%96%B9%E6%B3%95%EF%BC%8C%E4%BD%BF%E7%94%A8,%E7%9A%84%E5%90%8D%E5%AD%97%EF%BC%8C%E8%BF%99%E9%87%8C%E4%B8%BAdbuser%E3%80%82&text=%E7%84%B6%E5%90%8E%EF%BC%8C%E5%88%87%E6%8D%A2%E5%88%B0postgres%E7%94%A8%E6%88%B7%E3%80%82&text=%E4%B8%8B%E4%B8%80%E6%AD%A5%EF%BC%8C%E4%BD%BF%E7%94%A8psql%E5%91%BD%E4%BB%A4%E7%99%BB%E5%BD%95PostgreSQL%E6%8E%A7%E5%88%B6%E5%8F%B0%E3%80%82&text=%E8%BF%99%E6%97%B6%E7%9B%B8%E5%BD%93%E4%BA%8E%E7%B3%BB%E7%BB%9F,%E6%98%AF%E4%B8%8D%E7%94%A8%E8%BE%93%E5%85%A5%E5%AF%86%E7%A0%81%E7%9A%84%E3%80%82

### 基本pg操作

### step into / step over / step out之间的区别

https://www.ibm.com/support/pages/differences-between-step-over-step-and-step-out-commands

https://blog.csdn.net/huangfei711/article/details/51220382#:~:text=1771-,step%20into%EF%BC%9A%E5%8D%95%E6%AD%A5%E6%89%A7%E8%A1%8C%EF%BC%8C%E9%81%87%E5%88%B0%E5%AD%90%E5%87%BD%E6%95%B0%E5%B0%B1,%E5%AD%90%E5%87%BD%E6%95%B0%E6%95%B4%E4%B8%AA%E4%BD%9C%E4%B8%BA%E4%B8%80%E6%AD%A5%E3%80%82&text=%E6%9C%89%E4%B8%80%E7%82%B9%2C-,step%20out%EF%BC%9A%E5%BD%93%E5%8D%95%E6%AD%A5%E6%89%A7%E8%A1%8C%E5%88%B0%E5%AD%90%E5%87%BD%E6%95%B0%E5%86%85,%E7%94%A8step%20out%E5%B0%B1...



### 在pg中不能使用order作为字段名

建表的时候需要加双引号



### 在进行modification添加的时候，不能直接在db脚本的最后追加新的删表建表语句，因为直接删除父表是会报错的



6000欧元一平米，aix临近市中心的meuble



### 需求1：

在关闭页面并退回菜单的时候，如果数据没有提交，需要显示一个对话框——数据是否需要被录入到数据库，如果确实需要录入，那么将自动执行DB transfer

### 需求2：

在执行DB transfer之后需要返回状态告诉用户数据是否成功录入

creees权限的用户只能修改数据但不能使用数据

validee权限的用户只能使用数据但不能修改数据



### 需求3：

在确定数据库可使用之后，需要判断数据库中是否存在数据

如果不存在数据，那么按下cancel，如果存在数据，那么会使用插入数据语句，如果成功执行，那么归零

### 需求4：

cancel按钮是为了取消输入的数据

### 需求5：

在一些界面中search按钮可以帮助用户从文件中导入数据