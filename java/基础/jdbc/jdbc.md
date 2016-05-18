jdbc

与MySQL数据库连接的方法：

Connection con=DriverManager.getConnection(“jdbc:mysql://主机IP或主机名:3306/数据库名”,用户名，密码);

java.sql.DriveManager  用来处理装载驱动程序并且为创建新的数据库连接提供支持；

–java.sql.Connection  用于完成对特定定数据库的连接；

–java.sql.Statement  用于对特定的数据库执行SQL语句；java.sql.Statement又包含了以下两个重要的子类型：

       java.sql.PreparedStatement  用于执行预编译的SQL语句；

       java.sql.CallableStatement  用于执行数据库中存储的过程的调用；

--java.sql.ResultSet  用于保存查询所得的结果集

3、创建Statement对象

Statement  st=con.createStatement();  //最后可以不关闭，但推荐关闭

利用Statement对象可以执行静态SQL语句，静态SQL语句可以是Select语句、Delete语句、Update语句和Insert语句。

执行SQL语句

Statement接口提供了三种执行SQL语句的方法：executeQuery()、executeUpdate() 和execute()。具体使用哪一个方法由SQL语句本身来决定。

方法 executeQuery 用于产生单个结果集的语句，例如 SELECT 语句等。

方法 executeUpdate 用于执行INSERT、UPDATE或DELETE 语句以及SQL DDL（数据定义语言）语句，例如 CREATE TABLE 和 DROP TABLE。INSERT、UPDATE 或DELETE 语句的效果是修改表中零行或多行中的一列或多列。executeUpdate 的返回值是一个 整数，指示受影响的行数（即更新计数）

    ①JDBC在编译时并不对将要执行的SQL查询语句作任何检查，只是将其作为一个String类对象，直到驱动程序执行SQL查询语句时才知道其是否正确。对于错误的SQL查询语句，在执行时将会产生 SQLException。

    ②一个Statement对象在同一时间只能打开一个结果集，对第二个结果集的打开隐含着对第一个结果集的关闭。

    ③如果想对多个结果集同时操作，必须创建出多个Statement对象，在每个Statement对象上执行SQL查询语句以获得相应的结果集。

    ④如果不需要同时处理多个结果集，则可以在一个Statement对象上顺序执行多个SQL查询语句，对获得的结果集进行顺序操作。

4、分析ResultSet对象

① 执行完毕SQL语句后，将返回一个ResultSet类的对象，它包含所有的查询结果。但对ResultSet类的对象方式依赖于光标（Cursor）的 类型，而对每一行中的各个列，可以按任何顺序进行处理（当然，如果按从左到右的顺序对各列进行处理可以获得较高的执行效率）；

ResultSet类中的Course方式主要有：

ResultSet.TYPE_FORWARD_ONLY（为缺省设置）：光标只能前进不能后退，也就是只能从第一个一直移动到最后一个。

ResultSet.TYPE_SCROLL_SENSITIVE：允许光标前进或后退并感应到其它ResultSet的光标的移动情形。

ResultSet.TYPE_SCROLL_INSENSITIVE：允许光标前进或后退并不能感应到其它ResultSet的光标的移动情形。

ResultSet类中的数据是否允许修改主要有：

ResultSet.CONCUR_READ_ONLY（为缺省设置）：表示数据只能只读，不能更改。

ResultSet.CONCUR_UPDATABLE：表示数据允许被修改。

② ResultSet类的对象维持一个指向当前行的指针，利用ResultSet类的next()方法可以移动到下一行（在JDBC中，Java程序一次只 能看到一行数据），如果next()的返回值为false，则说明已到记录集的尾部。另外JDBC也没有类似ODBC 的书签功能的方法。

③ 利用ResultSet类的getXXX()方法可以获得某一列的结果，其中XXX代表JDBC中的Java数据类型，如 getInt()、getString()、getDate()等。访问时需要指定要检索的列（可以采用 int值作为列号（从1开始计数）或指定列（字段）名方式，但字段名不区别字母的大小写）。

5、关闭连接

(注意关闭的顺序） 例：

rs.close();

st.close();

con.close()


6、JDBC的常用API

一、Connection接口：

       1.createStatement()：创建数据库连接

       2.prepareStatement(Stringsql):创建预处理语句

       3.prepareCall(Stringsql):创建可调用语句

       4.getAutoCommit():获取自动提交的模式

       5.setAutoCommit():设置自动提交的模式

       6.commit():提交所执行的SQL语句

       7.rollback():回滚所执行的SQL语句

       8.getMetaData():获取一个DatabaseMetaData对象，该对象包含了有关数据库的基本信息

       9.close():关闭数据库连接

      10.isClose()：判断数据库连接是否超时或被显示关闭

二、Statement接口：

       1.execute(Stringsql):执行SQL语句，如果返回值是结果集则为true,否则为false

       2.executeQuery(Stringsql):执行SQL语句，返回值为ResultSet

       3.executeUpdate(Stringsql):执行SQL语句，返回值为所影响的行数

       4.addBatch(Stringsql):向当前Statement对象的命令列表中添加新的批处理SQL语句

       5.clearBatch():清空当前Statement对象的命令列表

       6.executeBatch()：执行当前Statement对象的批处理语句，返回值为每个语句所影响的函数数组

       7.getConnection():返回创建了该Statement对象的Connection对象

       8.getQueryTimeout():获取等待处理结果的时间

       9.setQueryTimeout():设置等待处理结果的时间

三、ResultSet接口：

       1.first()/beforeFirst():将游标移动到ResultSet中第一条记录(的前面)

       2.last()/afterLast():将游标移动到ResultSet中最后一条记录(的后面)

       3.absolute(intcolumn):将游标移动到相对于第一行的指定行，负数则为相对于最后一条记录

       4.relative(introws):将游标移动到相对于当前行的第几行,正为向下，负为向上

       5.next():将游标下移一行

       6.previous():将游标上移一行

       7.insertRow():向当前ResultSet和数据库中被插入行处插入一条记录

       8.deleteRow():将当前ResultSet中的当前行和数据库中对应的记录删除

       9.updateRow():用当前ResultSet中已更新的记录更新数据库中对应的记录

       10.cancelUpdate():取消当前对ResultSet和数据库中所做的操作

       11.findColumn(StringcolumnName):返回当前ResultSet中与指定列名对应的索引

       12.getRow():返回ResultSet中的当前行号

       13.refreshRow():更新当前ResultSet中的所有记录

       14.getMetaData():返回描述ResultSet的ResultSetMetaData对象

       15.isAfterLast():是否到了结尾

       16.isBeforeFirst(): 是否到了开头

       17.isFirst():是否第一条记录

       18.isLast(): 是否最后一条记录

       19.wasNull():检查列值是否为NULL值，如果列的类型为基本类型，且数据库中的值为0，那么

这项检查就很重要。由于数据库NULL也返回0，所以0值和数据库的NULL不能区分。如果列的类型为对象，可以简单地将返回值与null比较

        20.close():关闭当前ResultSet

四、ResultSetMetaData接口：

       1.getColumnCount():返回ResultSet中列的数目

       2.getColumnName():返回列在数据库中的名称

       3.getColumnType():返回列的SQL类型

       4.isReadOnly():表示该数据项是否为只读值

       5.isNullable():表示该列是否可以存储NULL






