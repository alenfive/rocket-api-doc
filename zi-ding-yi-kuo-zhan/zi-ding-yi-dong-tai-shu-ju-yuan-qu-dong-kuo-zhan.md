# 自定义动态数据源驱动扩展

1.  继承抽象类： 

    ```
    com.github.alenfive.rocketapi.datasource.factory
    ```


2. 可参考mysql驱动扩展

```
com.github.alenfive.rocketapi.datasource.factory.MySQLDriver
```



```
import com.github.alenfive.rocketapi.datasource.DataSourceDialect;
import com.github.alenfive.rocketapi.datasource.MySQLDataSource;
import com.github.alenfive.rocketapi.entity.DBConfig;
import org.springframework.stereotype.Component;

/**
 * SQL  构造器
 */
@Component    //需要注册为spring bean
public class MySQLDriver extends JdbcDriver {

    @Override
    public String getName() {    //驱动名称，全局唯一
        return "MySQL";
    }

    @Override
    public String getIcon() {    //定义驱动的图标
        return "rocketapi/images/mysql.png";
    }

    @Override
    public String getFormat() {    //驱动URL的格式
        return "jdbc:mysql://localhost:3306/test";
    }

    /**
    * DBConfig对象中的入参为界面数据源中的配置项，
    * 根据配置项自定义数据源的配置，要求返回`DataSourceDialect`
    */
    @Override                    
    public DataSourceDialect factory(DBConfig config) throws Exception {
        return new MySQLDataSource(super.getJdbcTemplate(config));
    }
}
```

 

3\. 启动程序后，所创建的驱动将会出现在新增数据源驱动列表中

![](<../.gitbook/assets/image (18).png>)
