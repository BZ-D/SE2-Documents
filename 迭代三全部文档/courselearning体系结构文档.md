# Course-Learning网站软件体系结构文档

## 文档修改历史

|                    修改人员                    |   日期   |        修改原因        | 版本号 |
| :--------------------------------------------: | :------: | :--------------------: | :----: |
|                     姬筠刚                     | 2021-7-5 |       创建该文档       |  0.1   |
|                     姬筠刚                     | 2021-7-6 | 完成自己分工的文档任务 | 0.1.1  |
| 往后的日期尽量写在7月8前，体现文档在代码前（笑 |          |                        |        |
|                                                |          |                        |        |
|                                                |          |                        |        |
|                                                |          |                        |        |
|                                                |          |                        |        |
|                                                |          |                        |        |
|                                                |          |                        |        |
|                                                |          |                        |        |
|                                                |          |                        |        |
|                                                |          |                        |        |

## 目录

[TOC]




## 1. 引言

### 1.1 编制目的

本软件体系结构描述文档对课程学习网站“Course Learning迭代三”进行了系统、详细的概要设计，主要目标是对该课程学习网站的详细设计和开发进行指导，并便于测试人员和用户进行沟通。

本文档面向开发人员、测试人员及最终用户编写，是相关人员了解“Course Learning”迭代三的导航。

### 1.2 词汇表

|    词汇名称     |    词汇含义    |                    备注                    |
| :-------------: | :------------: | :----------------------------------------: |
| Course Learning |    课程学习    |             是该系统的英文名称             |
|    HTTP REST    | 表述性状态传递 |     是一种针对网络应用的设计和开发方式     |
|       UI        |    用户接口    | 即User Interface，用户界面，人机交互的媒介 |
|       BL        |    业务逻辑    |   即Business Logic，是层次体系中的中间层   |

### 1.3 参考资料

- 骆斌，丁二玉，刘钦. 软件工程与计算.卷二,软件开发的技术基础.volume Ⅱ, Fundamentals of software development technology[M]. 机械工业出版社, 2012.
- 课程学习网站(Courselearning)用例文档 V-1.0。
- 课程学习网站(Courselearning)需求规格说明文档 V-1.0。

## 2. 产品概述

课程学习网站"Course-Learning"是为高校学生及开设高等学校课程的教师开发的课程学习、管理系统，开发目标是为高校学生提供一个线上进行课程学习的平台，并且为高校教师提供一个线上发布课程、灵活管理课程的平台。

通过课程学习网站"Course-Learning"的应用，期望帮助高校学生提高学习效率、拓宽知识面、进行专业课程循序渐进学习，帮助相关教师推广课程、更便利地利用互联网资源进行教学。

## 3. 逻辑视图

课程学习网站系统中，选择分层体系结构风格，将系统分为3层（展示层Presentation，业务逻辑层Businesslogic及数据层Data），能够很好地示意整个高层抽象。展示层包含GUI页面的实现，业务逻辑层包含业务逻辑处理的实现，数据层负责数据的持久化和访问。分层体系结构的逻辑视角和逻辑设计方案见下二图。

- ##### 参照体系结构风格的包图表达逻辑视角

<img src="https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/逻辑视角.png" style="zoom:67%;" />



- ##### 软件体系结构逻辑设计方案（详细设计包图）

![总体详细包图](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/%E6%80%BB%E4%BD%93%E8%AF%A6%E7%BB%86%E5%8C%85%E5%9B%BE.jpg)

## 4. 组合视图

### 4.1 开发包图

#### 前端开发包图

"Course-Learning"课程学习网站系统迭代三的前端开发包图如下图所示：

![迭代三前端开发包图](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/%E8%BF%AD%E4%BB%A3%E4%B8%89%E5%89%8D%E7%AB%AF%E5%BC%80%E5%8F%91%E5%8C%85%E5%9B%BE.jpg)

#### 后端开发包图

"Course-Learning"课程学习网站系统迭代三的后端开发包图如下图所示：

![迭代三后端开发包图](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/%E8%BF%AD%E4%BB%A3%E4%B8%89%E5%90%8E%E7%AB%AF%E5%BC%80%E5%8F%91%E5%8C%85%E5%9B%BE.jpg)

### 4.2 运行时进程

在课程学习网站(Course-learning)中，会有多个客户端进程和一个服务器端进程，其进程图如下图所示。结合部署图，客户端进程是在客户端机器上运行，服务器端进程在服务器端机器上运行。

- 进程示意图：

  <img src="https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/进程图.png" alt="进程图" style="zoom:50%;" />


### 4.3 物理部署

课程学习网站(Course-learning)中客户端构建是放在客户端机器上，服务器端构件是放在服务器端机器上。客户端和服务器端之间通过http rest通信。在系统JDK环境已经设置好的情况下，不需要再独立部署。

- 部署图如下图所示。

![部署图](https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/部署图.png)



## 5. 架构设计

### 5.1 模块职责

#### 5.1.1 模块视图

![模块视图](https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/模块视图.png)

#### 5.1.2 各层职责

##### 表1 客户端各层的职责

|       层       | 职责                                                                   |
| :------------: | ---------------------------------------------------------------------- |
|    启动模块    | 负责初始化网络通信机制，初始化网页前端、后端和数据库，展现用户展示网页 |
|   用户界面层   | 基于前端、后端和数据库的课程学习（Course-learning）网站用户展示网页    |
|   业务逻辑层   | 对于学生和老师用户的鼠标点击和键盘输入操作进行响应并进行业务处理逻辑   |
| 客户端网络模块 | 依赖http rest和服务器端进行通信                                        |

#####       表2 服务器端各层的职责

| 层               | 职责                                                                   |
| ---------------- | ---------------------------------------------------------------------- |
| 启动模块         | 负责初始化网络通信机制，初始化网页前端、后端和数据库，展现用户展示网页 |
| 数据层           | 负责数据的持久化及数据访问接口                                         |
| 服务器端网络模块 | 依赖http rest和客户端进行通信                                          |

​		每一层只是使用下方直接接触的层。层与层之间仅仅是通过接口的调用来完成的。层之间调用的接口如表3所示。

层之间调用接口

##### 表3 层之间调用的接口

|                                                                        接口                                                                         | 服务调用方       | 服务提供方       |
| :-------------------------------------------------------------------------------------------------------------------------------------------------: | ---------------- | ---------------- |
|    UserBLService<br />RechargeBLService<br />Course_OrderBLService<br />Course_wareBLService<br />Course_manageBLService<br />PromotionBLService    | 客户端展示层     | 客户端业务逻辑层 |
| UserDataService<br />RechargeDataService<br />Course_OrderDataService<br />Course_WareDataService<br />Course_DataService<br />PromotionDataService | 客户端业务逻辑层 | 服务器端数据层   |

### 5.2 用户界面层分解

#### 5.2.1 职责

- 类图

  根据需求，系统存在8个用户界面：未登录状态下的课程展示界面、登录界面、注册界面、学生用户主界面、历史订单界面、学生用户个人中心界面、老师用户界面、老师用户个人中心界面

  ![用户界面跳转](https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/用户界面跳转.png)

  ​                                                                                           **图 用户界面跳转**

- 接口规范

  ##### 表4 用户界面层模块的接口规范

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

  ##### 表5 用户界面层模块需要的服务接口

|          服务名          | 服务                               |
| :----------------------: | ---------------------------------- |
| BLService.LoginBLService | 登录界面的业务逻辑接口             |
|   BLService.*BLService   | 每个界面都有一个相应的业务逻辑接口 |

### 5.3 业务逻辑层的分解

业务逻辑层的设计如图所示。

![业务逻辑层设计类图](https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/业务逻辑层设计类图.png)

#### 5.3.1 业务逻辑层模块的职责

业务逻辑层模块的职责如下表所示。

| 模块            | 职责                                                                                                         |
| --------------- | ------------------------------------------------------------------------------------------------------------ |
| userbl          | 负责用户注册、登录、获取用户信息界面所需要的服务                                                             |
| rechargebl      | 负责用户充值界面所需要的服务                                                                                 |
| course_orderbl  | 负责生成课程订单、更新订单状态、获取用户订单界面所需要的服务                                                 |
| couse_warebl    | 负责用户获取课件、创建课件、更新课件、删除课件界面所需要的服务                                               |
| course_managebl | 负责获取课程、分页获取课程列表、获取用户已购买的课程列表、获取教师可管理的课程列表、创建课程界面所需要的服务 |
| promotionbl     | 负责使用优惠券购买课程界面、发布优惠券、发布优惠课程界面所需要的服务                                         |

#### 5.3.2业务逻辑层模块的接口规范

- **userbl模块**的接口规范如下表所示：

**提供的服务（供接口）**

<table>
	<tr >
	    <td rowspan="3">userRegister</td>
	    <td>语法</td>
	    <td>ResultVO<UserVO> userRegister(UserVO user);</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>注册信息正确且符合输入规则</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>数据库中存入新注册用户的信息</td>
	</tr>
     <tr >
        <td rowspan="3">userLogin</td>
        <td>语法</td>
        <td>ResultVO<UserVO> userLogin(String phone, String password);</td>
    </tr>
    <tr>
        <td>前置条件</td>
        <td>phone、password符合输入规则</td>
    </tr>
    <tr>
        <td>后置条件</td>
        <td>查找是否存在相应的User，根据输入的password返回登录验证的结果</td>
    </tr>
    <tr >
        <td rowspan="3">getUser</td>
        <td>语法</td>
        <td>UserVO getUser(Integer uid);</td>
    </tr>
    <tr>
        <td>前置条件</td>
        <td>用户id符合输入规则</td>
    </tr>
    <tr>
        <td>后置条件</td>
        <td>查找是否存在相应的User，根据输入的用户id返回用户信息</td>
    </tr>
    </table>


| 需要的服务（需接口）               |                              |
| ---------------------------------- | ---------------------------- |
| 服务名                             | 服务                         |
| userMapper.selectByPhone(phone)    | 根据用户phone值查找用户      |
| userMapper.selectByPrimaryKey(uid) | 根据用户id查找用户信息       |
| userMapper.insert(user)            | 向数据库中插入新注册用户数据 |



- **rechargebl模块**的接口规范如下表所示：

**提供的服务（供接口）**

<table>
	<tr >
	    <td rowspan="3">rechargeAccount</td>
	    <td>语法</td>
	    <td>ResultVO<UserVO> rechargeAccount(RechargeOrderVO rechargeOrderVO);</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>充值数额符合输入规则</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>修改用户的余额</td>
	</tr>
    </table>


| 需要的服务（需接口）                      |              |
| ----------------------------------------- | ------------ |
| 服务名                                    | 服务         |
| userMapper.increaseBalance(userId, value) | 更新用户余额 |
| rechargeOrderVO.getUserId()               | 找到充值用户 |



- **course_orderbl模块**的接口规范如下表所示：

**提供的服务（供接口）**

<table>
	<tr >
	    <td rowspan="3">insertCourseOrder</td>
	    <td>语法</td>
	    <td>ResultVO<CourseOrderVO> insertCourseOrder(CourseOrderVO orderVO);</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>用户购买课程</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>保存订单信息</td>
	</tr>
     <tr >
        <td rowspan="3">updateCourseOrder</td>
        <td>语法</td>
        <td>ResultVO<CourseOrderVO> updateCourseOrder(Integer orderId, Integer orderStatus);</td>
    </tr>
    <tr>
        <td>前置条件</td>
        <td>用户支付订单</td>
    </tr>
    <tr>
        <td>后置条件</td>
        <td>更新用户课程权限</td>
    </tr>
    <tr >
        <td rowspan="3">getCourseOrders</td>
        <td>语法</td>
        <td>List<CourseOrderVO> getCourseOrders(Integer uid);</td>
    </tr>
    <tr>
        <td>前置条件</td>
        <td>用户已经验证登录</td>
    </tr>
    <tr>
        <td>后置条件</td>
        <td>返回用户订单列表</td>
    </tr>
    </table>


| 需要的服务（需接口）                                                         |                  |
| ---------------------------------------------------------------------------- | ---------------- |
| 服务名                                                                       | 服务             |
| orderMapper.queryMostRecentOrder(orderVO.getUserId(), orderVO.getCourseId()) | 查询用户购买权限 |
| userMapper.selectByPrimaryKey(order.getUserId())                             | 查找用户         |
| userMapper.decreaseBalance(user.getId(), order.getCost())                    | 更新用户账户余额 |
| orderMapper.insert(order)                                                    | 增加订单记录     |
| orderMapper.selectByPrimaryKey(orderId)                                      | 查找订单         |
| orderMapper.updateByPrimaryKey(order)                                        | 更新订单记录     |



- **couse_warebl模块**的接口规范如下表所示：

**提供的服务（供接口）**

<table>
	<tr >
	    <td rowspan="3">getCourseWare</td>
	    <td>语法</td>
	    <td>CourseWareVO getCourseWare(Integer uid, Integer courseWareId);</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>进入到网页，点击课件</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>返回课件信息</td>
	</tr>
     <tr >
        <td rowspan="3">createCourseWare</td>
        <td>语法</td>
        <td>ResultVO<CourseWareVO> createCourseWare(CourseWareVO courseWareVO);</td>
    </tr>
    <tr>
        <td>前置条件</td>
        <td>登录为教师用户</td>
    </tr>
    <tr>
        <td>后置条件</td>
        <td>生成课件</td>
    </tr>
    <tr >
        <td rowspan="3">updateCourseWare</td>
        <td>语法</td>
        <td>ResultVO<CourseWareVO> updateCourseWare(CourseWareVO courseWareVO);</td>
    </tr>
    <tr>
        <td>前置条件</td>
        <td>登录为教师用户</td>
    </tr>
    <tr>
        <td>后置条件</td>
        <td>更新课件</td>
    </tr>
    <tr >
        <td rowspan="3">deleteCourseWare</td>
        <td>语法</td>
        <td>ResultVO<String> deleteCourseWare(Integer courseWareId);</td>
    </tr>
    <tr>
        <td>前置条件</td>
        <td>登录为教师用户</td>
    </tr>
    <tr>
        <td>后置条件</td>
        <td>删除课件</td>
    </tr>
    </table>


| 需要的服务（需接口）                                  |                      |
| ----------------------------------------------------- | -------------------- |
| 服务名                                                | 服务                 |
| courseWareMapper.selectByPrimaryKey(courseWareId)     | 查找课件             |
| courseOrderMapper.queryMostRecentOrder(uid, courseId) | 确认用户查看课件权限 |



- **course_managebl模块**的接口规范如下表所示：

**提供的服务（供接口）**

<table>
	<tr >
	    <td rowspan="3">createCourse</td>
	    <td>语法</td>
	    <td>ResultVO<CourseVO> createCourse(CourseVO courseVO);</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>进入到网页，登录为教师用户</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>生成新课程</td>
	</tr>
     <tr >
        <td rowspan="3">getCourses</td>
        <td>语法</td>
        <td>PageInfo<CourseVO> getCourses(Integer currPage, Integer pageSize, Integer uid, String key);</td>
    </tr>
    <tr>
        <td>前置条件</td>
        <td>入到网页，输入关键字</td>
    </tr>
    <tr>
        <td>后置条件</td>
        <td>根据关键字分页返回课程信息</td>
    </tr>
    <tr >
        <td rowspan="3">getCourse</td>
        <td>语法</td>
        <td>CourseVO getCourse(Integer courseId, Integer uid);</td>
    </tr>
    <tr>
        <td>前置条件</td>
        <td>进入到网页，点击课程</td>
    </tr>
    <tr>
        <td>后置条件</td>
        <td>返回课程信息</td>
    </tr>
    </table>


| 需要的服务（需接口）                                    |                      |
| ------------------------------------------------------- | -------------------- |
| 服务名                                                  | 服务                 |
| courseMapper.queryAll(key)                              | 根据关键字查找课程   |
| courseMapper.selectByPrimaryKey(courseId)               | 根据课程编号查找课程 |
| courseMapper.selectByTeacherId(courseVO.getTeacherId()) | 根据课程教师查找课程 |

### 5.4 数据层的分解

数据层模块的描述如图所示。

![数据层模块描述](https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/数据层模块描述.png)

#### 5.4.1 数据层模块的职责

| 模块                | 职责                                               |
| ------------------- | -------------------------------------------------- |
| UserMapper          | 负责用户信息的增、删、查、改，以及更改用户余额服务 |
| RechargeOrderMapper | 负责充值交易的更新服务                             |
| CourseWareMapper    | 负责课件的增、删、改、查服务                       |
| CourseOrderMapper   | 负责订单信息的增、删、改、查服务                   |
| CourseMapper        | 负责课程信息的增、删、改、查服务                   |

#### 5.4.2 数据层模块的接口规范

数据层模块的接口规范如下表所示：

<table>
	<tr >
	    <td rowspan="3">CourseMapper.insert</td>
	    <td>语法</td>
	    <td>int insert(Course record);</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>课程信息符合输入规则</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>在数据库中添加课程信息</td>
	</tr>
     <tr >
        <td rowspan="3">CourseMapper.deleteByPrimaryKey</td>
        <td>语法</td>
        <td>int deleteByPrimaryKey(Integer id);</td>
    </tr>
    <tr>
        <td>前置条件</td>
        <td>系统中存在该课程</td>
    </tr>
    <tr>
        <td>后置条件</td>
        <td>系统删除该课程</td>
    </tr>
    <tr >
        <td rowspan="3">CourseMapper.updateByPrimaryKey</td>
        <td>语法</td>
        <td>int updateByPrimaryKey(Course record);</td>
    </tr>
    <tr>
        <td>前置条件</td>
        <td>系统中存在该课程</td>
    </tr>
    <tr>
        <td>后置条件</td>
        <td>系统更新课程信息</td>
    </tr>
    <tr >
	    <td rowspan="3">UserMapper.insert</td>
	    <td>语法</td>
	    <td>int insert(User record);</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>用户数据符合输入规则</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>在数据库中添加用户信息</td>
	</tr>
     <tr >
        <td rowspan="3">UserMapper.increaseBalance</td>
        <td>语法</td>
        <td>void increaseBalance(@Param(value = "id") Integer id, @Param(value = "delta")Integer delta);</td>
    </tr>
    <tr>
        <td>前置条件</td>
        <td>余额符合输入规则</td>
    </tr>
    <tr>
        <td>后置条件</td>
        <td>修改用户账户余额</td>
    </tr>
    <tr >
        <td rowspan="3">CourseOrderMapper.queryMostRecentOrder</td>
        <td>语法</td>
        <td>CourseOrder queryMostRecentOrder(Integer userId, Integer courseId);</td>
    </tr>
    <tr>
        <td>前置条件</td>
        <td>用户id、课程id符合输入规则</td>
    </tr>
    <tr>
        <td>后置条件</td>
        <td>返回课程查找结果</td>
    </tr>
    </table>



## 6. 信息视角

### 6.1 数据持久化对象

系统的PO类就是对应相关的实体类，下面将对这些实体类作一些介绍。

- UserPO类包含用户的用户名、手机号码、密码、账户余额、用户角色、账号创建时间
- CoursePO类包含课程类型、课程简介、所属学校、创建/删除时间、课程价格、教师姓名
- CourseOrderPO类包含订单金额、课程名称、订单创建时间、支付状态
- CourseWarePO类包括课件题目、课件名称、上传时间、课件类型、课件大小
- RechargeOrderPO类包括充值金额、充值时间、充值用户
- PromotionPO类包括优惠时间、优惠额度、优惠适用课程

下以持久化对象CoursePO的定义为例。

```java
public class Course {
    private Integer id;
    private String name;
    private String type;
    private String intro;
    private String picture;
    private String school;
    private Date createTime;
    private Date deleteTime;
    private Integer cost;
    private Integer teacherId;
    private String teacherName;

    public Integer getId() {
        return id;
    }
    public void setId(Integer id) {
        this.id = id;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name == null ? null : name.trim();
    }
    public String getType() {
        return type;
    }
    public void setType(String type) {
        this.type = type == null ? null : type.trim();
    }
    public String getIntro() {
        return intro;
    }
    public void setIntro(String intro) {
        this.intro = intro == null ? null : intro.trim();
    }
    public String getPicture() {
        return picture;
    }
    public void setPicture(String picture) {
        this.picture = picture == null ? null : picture.trim();
    }
    public String getSchool() {
        return school;
    }
    public void setSchool(String school) {
        this.school = school == null ? null : school.trim();
    }
    public Date getCreateTime() {
        return createTime;
    }
    public void setCreateTime(Date createTime) {
        this.createTime = createTime;
    }
    public Date getDeleteTime() {
        return deleteTime;
    }
    public void setDeleteTime(Date deleteTime) {
        this.deleteTime = deleteTime;
    }
    public Integer getCost() {
        return cost;
    }
    public void setCost(Integer cost) {
        this.cost = cost;
    }
    public Integer getTeacherId() {
        return teacherId;
    }
    public void setTeacherId(Integer teacherId) {
        this.teacherId = teacherId;
    }
    public String getTeacherName() {
        return teacherName;
    }
    public void setTeacherName(String teacherName) {
        this.teacherName = teacherName == null ? null : teacherName.trim();
    }
}
```

### 6.2 数据库表

课程学习网站系统的数据库中包含以下表：

<img src="https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/数据库表.png" style="zoom:67%;" />