# 软件体系结构文档模板

## 组合视图


### 运行时进程

- 在课程学习网站(Course-learning)中，会有多个客户端进程和一个服务器端进程，其进程图如下图所示。结合部署图，客户端进程是在客户端机器上运行，服务器端进程在服务器端机器上运行。

  - 绘制进程图

- 示意图：

  ![进程图](https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/进程图.png)


### 物理部署

- 课程学习网站(Course-learning)中客户端构建是放在客户端机器上，服务器端构件是放在服务器端机器上。在客户端节点上， 还要部署RMIStub构件。由于Java RMI构件属千JDK8.0的一部分。所以，在系统JDK环境已经设置好的清况下，不需要再独立部署。部署图如下图所示。
  - 绘制部署图
- 示意图

![icon](http://assets.processon.com/chart_image/5ae5be27e4b039625af793c0.png?_=1554259679134)

## 架构设计

- 描述功能分解和如何在不同的层中安排软件模块
  - 描述架构中的对象，包含架构图
  - 描述组件接口信息
    - 包括：语法、前置条件、后置条件

### 模块职责

- 模块视图

  ![模块视图](https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/模块视图.png)

- 各层职责

  ###### 表1 客户端各层的职责

|       层       | 职责                                                         |
| :------------: | ------------------------------------------------------------ |
|    启动模块    | 负责初始化网络通信机制，初始化网页前端、后端和数据库，展现用户展示网页 |
|   用户界面层   | 基于前端、后端和数据库的课程学习（Course-learning）网站用户展示网页 |
|   业务逻辑层   | 对于学生和老师用户的鼠标点击和键盘输入操作进行响应并进行业务处理逻辑 |
| 客户端网络模块 | 利用Java RMI机制查找RMI服务                                  |

######       表2 服务器端各层的职责

| 层               | 职责                                                         |
| ---------------- | ------------------------------------------------------------ |
| 启动模块         | 负责初始化网络通信机制，初始化网页前端、后端和数据库，展现用户展示网页 |
| 数据层           | 负责数据的持久化及数据访问接口                               |
| 服务器端网络模块 | 利用Java RMI机制开启RMI服务，注册RMI服务                     |

​		每一层只是使用下方直接接触的层。层与层之间仅仅是通过接口的调用来完成的。层之间调用的接口如表3所示。

- 层之间调用接口

  ###### 表3 层之间调用的接口

|                             接口                             | 服务调用方       | 服务提供方       |
| :----------------------------------------------------------: | ---------------- | ---------------- |
| UserBLService<br />RechargeBLService<br />Course_OrderBLService<br />Course_wareBLService<br />Course_manageBLService<br />PromotionBLService | 客户端展示层     | 客户端业务逻辑层 |
| UserDataService<br />RechargeDataService<br />Course_OrderDataService<br />Course_wareDataService<br />Course_DataService<br />PromotionDataService | 客户端业务逻辑层 | 服务器端数据层   |



### 用户界面层分解

#### 职责

- 类图

  ​	根据需求，系统存在8个用户界面：未登录状态下的课程展示界面、登录界面、注册界面、学生用户主界面、历史订单界面、学生用户个人中心界面、老师用户界面、老师用户个人中心界面

  ![用户界面跳转](https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/用户界面跳转.png)

  ​                                                                                           **图 用户界面跳转**

- 接口规范

  ###### 表4 用户界面层模块的接口规范

<table>
	<tr >
	    <td rowspan="3">CourseLearningApplication</td>
	    <td>语法</td>
	    <td>init(args:String[])</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>初始化数据库</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>运行前端，显示未登录下的课程展示界面</td>
	</tr>
</table>

  

- 需要的服务接口

  ###### 表5 用户界面层模块需要的服务接口

|          服务名          | 服务                               |
| :----------------------: | ---------------------------------- |
| BLService.LoginBLService | 登录界面的业务逻辑接口             |
|   BLService.*BLService   | 每个界面都有一个相应的业务逻辑接口 |

