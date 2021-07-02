## 项目开发准备工作

1. 搭建一个maven.xml项目

2. 配置Tomcat

3. 测试项目是否能运行

4. 导入项目中需要的jar包

   jsp.Servlet.mysql驱动，jstl，standard

5. 创建项目包结构

6. 编写实体类

   ORM映射：表-类映射

7. 编写基础公共类

   1. 数据库配置文件

      ```properties
      driver=com.mysql.jdbc.Driver
      url=jdbc:mysql://localhost:3306?useUnicode=true&characterEncoding=utf-8
      username=root
      password=123456
      ```

      

   2. 编写数据库的公共类

      ```java
      package com.niko.dao;
      
      import java.io.IOException;
      import java.io.InputStream;
      import java.sql.*;
      import java.util.Properties;
      
      public class BaseDao {
          private static String driver;
          private static String url;
          private static String username;
          private static String password;
      
          static{
              Properties properties = new Properties();
              // 通过类加载器获取对应数据
              InputStream is = BaseDao.class.getClassLoader().getResourceAsStream("db.properties");
              try {
                  properties.load(is);
              } catch (IOException e) {
                  e.printStackTrace();
              }
              driver = properties.getProperty("driver");
              url = properties.getProperty("url");
              username = properties.getProperty("username");
              password = properties.getProperty("password");
          }
      
          // 获取数据库的连接
          public static Connection getConnection(){
              Connection connection = null;
              try {
                  Class.forName(driver);
                  connection = DriverManager.getConnection(url,username,password);
              } catch (Exception e) {
                  e.printStackTrace();
              }
              return connection;
          }
      
          //编写查询公共类
          public static ResultSet execute(Connection connection,String sql,Object[] param) throws SQLException {
              PreparedStatement ps = connection.prepareStatement(sql);
              for(int i = 0; i < param.length; i++){
                  ps.setObject(i + 1, param[i]);
              }
              ResultSet rs = ps.executeQuery();
              return rs;
          }
      
          // 编写增删改查公共类
          public static int executeUpdate(Connection connection,String sql,Object[] param) throws SQLException {
              PreparedStatement ps = connection.prepareStatement(sql);
              for(int i = 0; i < param.length; i++){
                  ps.setObject(i + 1, param[i]);
              }
              int rs = ps.executeUpdate();
              return rs;
          }
      
          //释放资源
          public static void close(Connection con, PreparedStatement ps,ResultSet rs){
              
              if(rs != null){
                  try {
                      rs.close();
                      ps.close();
                      con.close();
                  } catch (SQLException throwables) {
                      throwables.printStackTrace();
                  }
              }
          }
      }
      ```

      

   3. 编写字符编码过滤器

8. 导入静态资源