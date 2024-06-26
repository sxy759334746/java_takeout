## Java项目学习

java外卖业务项目学习

使用SpringBoot Redis MyBatis MySQL Nginx SpringTask Swagger JWT 

前端微信小程序


## Nginx

- 反向代理配置
- 负载均衡： 
- 权重，ip哈希，最少连接，url哈希，响应时间


## 登录密码加密

- 返回password MD5加密


## apifox

- 导入接口文档


## Swagger

- ### 属性配置类 @ConfigurationProperties(perfix = xx.xxx)
- 属性配置类 加这个注解可以将application.yml文件里的配置读取并写java类里
- application文件可以引用a-dev.yml a-prod.yml 使用\${}传递值
- 
- knife4j 生成接口文档
- 常用注解：@Api @ApiModel @ApiModelProperty @ApiOperation
- 在doc.html 进行调试，添加全局参数token

## 员工数据CURD

- 全局异常处理
- jwt获取当前登录用户id
- ThreadLocal set() get() remove()
- ### 员工分页查询 
- 用到mybatis的pagehelpers  pom中添加依赖
- PageHelper.startPage() 添加page和pagesize参数
- page.getTotal()   getResult()
- 在mapper层声明sql方法 在xml文件中查询 \<select id="" resultType="">
- ### 配置springMVC的消息转换器
- 单独在entity类的日期属性上添加JsonFormat(pattern="yyyy-MM-dd HH:mm:ss")
- springMVC的消息转换器 给日期格式化
- 重写WebMvcConfigurationSupport中的方法 扩展消息转换器 用来给后端返回前端的数据进行统一处理
- common类里已经写好了一个对象转换器 这个转换器实现了几个序列化和反序列化 将几个时间格式给转换了 
- 将自己写的转换器加入容器中 
- 消息转换器是有顺序的，新添加的在最后 index为0表示放第一位

## 用AOP切面来完成 公共字段的填充

- 自定义注解 AutoFill 标识公共字段填充方法
- 注解AutoFill 加@Target(ElementType.METHOD) 表明af添加在方法上
- 枚举操作类型 OperationType类 只有UPDATE 和 INSERT
- ### 自定义切面类AutoFillAspect 
- 切入点匹配Mapper包下所有的类 所有方法 所有返回值类型
- @Pointcut("execution(* com.sky.mapper.*.*(..)) && @annotation(com.sky.annotation.AutoFill)")
- \&& 后边的表示需要匹配到添加了这个注解的方法
- 前置通知
- 获取当前被拦截方法的参数--实体对象