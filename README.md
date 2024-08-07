## Java项目学习

java外卖业务项目学习

- 使用SpringBoot Redis MyBatis MySQL SpringCache WebSocket Nginx SpringTask Swagger JWT 
- 前端微信小程序
- 具体实现见commit

## Nginx

- 反向代理配置
- 负载均衡： 
- 权重，ip哈希，最少连接，url哈希，响应时间


## Redis

- redis中的数据类型：字符串string 哈希hash 列表list 集合set 有序集合sorted set/zset
- spring-data-redis
- 导入maven坐标， 配置redis数据源， 写配置类创建RedisTemplate对象，通过RT操作Redis 
- 字符串操作命令 opsForValue()...


## Swagger

- ### 属性配置类 @ConfigurationProperties(perfix = xx.xxx)
- 属性配置类 加这个注解可以将application.yml文件里的配置读取并写java类里
- application文件可以引用a-dev.yml a-prod.yml 使用\${}传递值
- knife4j 生成接口文档
- 常用注解：@Api @ApiModel @ApiModelProperty @ApiOperation
- 在doc.html 进行调试，添加全局参数token


## 员工数据CRUD

- 全局异常处理
- ### jwt登录校验
- JwtProperties 封装jwt生成需要的属性 SecretKey Ttl
- 登录时候生成jwt令牌 后续请求由拦截器解析校验 JwtUtil.createJWT JwtUtil.parseJWT
- 使用ThreadLocal存取员工id  set() get() remove()
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


## 登录密码加密

- 返回password MD5加密


## apifox

- 导入接口文档
- 调试加全局参数token

## 阿里云oss对象存储

- 配置yml文件 application-dev版本 application.yml调用${}
- ConditionalOnMissingBean 只存在一个此类bean


## 菜品以及分类CRUD

- @RequestParam注解 将接收到的参数列表封装到 被注解的集合中


## 设置店铺状态以及接入小程序

- RequestController()设置名字区分不同包下的同名controller类


## HttpClient

- 导入maven坐标
HttpClient HttpClients CloseableHttpClient HttpGet HttpPost
- CloseableHttpClient HttpGet CloseableHttpResponse getStatusLine().getStatus() getEntity()


## 微信登录

- wx.login()获取code wx.request()发送code到后端
- 后端服务 调用微信接口服务 HttpClient请求 appid secret js_code grant_type


## Spring Cache 缓存

- SpringCache可以使用EHChche Caffeine Redis 通过maven坐标配置
- @EnableCaching 启动类注解开启缓存注解功能
- @Cacheable 方法执行前先查缓存，有则返回，没有则返回值放到缓存中
- @CachePut 将方法返回值放缓存中
- @CacheEvict 删除一条或多条缓存


## 用户购物车，下单，地址本CRUD


## 微信支付

- JSAPI 
- SpringTask任务调度
- coplar内网穿透 用来微信向后端推送支付结果请求


## SpringTask

- cron表达式 每个域的含义分别为：秒、分钟、小时、日、月、周、年(可选)
- @EnableScheduling 启动类加注解开启任务调度
- @Scheduled(cron = "  ")


## 百度地图API校验配送距离

- application.yml配置ak和地址
- @Values 得到配置文件值
- HttpClient向API发送请求
- 解析json


## WebSocket

- 导入WebSocket的maven坐标
- 导入WebSocket服务端组件WebSocketServer，用于和客户端通信
- 导入配置类WebSocketConfiguration，注册WebSocket的服务端组件
- 导入定时任务类WebSocketTask，定时向客户端推送数据
- onOpen onMessage onClose sendToAllClient
- 配置类内 ServerEndpointExporter方法，添加Bean注解 然后return new ServerEndpointExporter();