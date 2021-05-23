### 5.3 业务逻辑层的分解

业务逻辑层的设计如图所示。

![业务逻辑层设计类图](https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/业务逻辑层设计类图.png)

#### 5.3.1 业务逻辑层模块的职责

业务逻辑层模块的职责如下表所示。

| 模块            | 职责                                                         |
| --------------- | ------------------------------------------------------------ |
| userbl          | 负责用户注册、登录、获取用户信息界面所需要的服务             |
| rechargebl      | 负责用户充值界面所需要的服务                                 |
| course_orderbl  | 负责生成课程订单、更新订单状态、获取用户订单界面所需要的服务 |
| couse_warebl    | 负责用户获取课件、创建课件、更新课件、删除课件界面所需要的服务 |
| course_managebl | 负责获取课程、分页获取课程列表、获取用户已购买的课程列表、获取教师可管理的课程列表、创建课程界面所需要的服务 |
| promotionbl     | 负责使用优惠券购买课程界面、发布优惠券、发布优惠课程界面所需要的服务 |

#### 5.3.2业务逻辑层模块的接口规范

**userbl模块**的接口规范如下表所示：

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

**rechargebl模块**的接口规范如下表所示：

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

**course_orderbl模块**的接口规范如下表所示：

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

| 需要的服务（需接口）                                         |                  |
| ------------------------------------------------------------ | ---------------- |
| 服务名                                                       | 服务             |
| orderMapper.queryMostRecentOrder(orderVO.getUserId(), orderVO.getCourseId()) | 查询用户购买权限 |
| userMapper.selectByPrimaryKey(order.getUserId())             | 查找用户         |
| userMapper.decreaseBalance(user.getId(), order.getCost())    | 更新用户账户余额 |
| orderMapper.insert(order)                                    | 增加订单记录     |
| orderMapper.selectByPrimaryKey(orderId)                      | 查找订单         |
| orderMapper.updateByPrimaryKey(order)                        | 更新订单记录     |

**couse_warebl模块**的接口规范如下表所示：

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

**course_managebl模块**的接口规范如下表所示：

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

### 5.4数据层的分解

数据层模块的描述如图所示。

![数据层模块描述](https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/数据层模块描述.png)

#### 5.4.1数据层模块的职责

| 模块                | 职责                                               |
| ------------------- | -------------------------------------------------- |
| UserMapper          | 负责用户信息的增、删、查、改，以及更改用户余额服务 |
| RechargeOrderMapper | 负责充值交易的更新服务                             |
| CourseWareMapper    | 负责课件的增、删、改、查服务                       |
| CourseOrderMapper   | 负责订单信息的增、删、改、查服务                   |
| CourseMapper        | 负责课程信息的增、删、改、查服务                   |

#### 5.4.2数据层模块的接口规范

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
