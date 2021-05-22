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
| promotionbl     | 负责发布优惠券、发布优惠课程界面所需要的服务                 |

#### 5.3.2业务逻辑层模块的接口规范

**userbl模块**的接口规范如下表所示：

| 提供的服务（供接口） |          |                                                              |
| :------------------: | :------: | :----------------------------------------------------------: |
|                      |   语法   |         ResultVO<UserVO> userRegister(UserVO user);          |
|     userRegister     | 前置条件 |                  注册信息正确且符合输入规则                  |
|                      | 后置条件 |                 数据库中存入新注册用户的信息                 |
|                      |          |                                                              |
|                      |   语法   |  ResultVO<UserVO> userLogin(String phone, String password);  |
|      userLogin       | 前置条件 |                 phone、password符合输入规则                  |
|                      | 后置条件 | 查找是否存在相应的User，根据输入的password返回登录验证的结果 |
|                      |          |                                                              |
|                      |   语法   |                 UserVO getUser(Integer uid);                 |
|       getUser        | 前置条件 |                      用户id符合输入规则                      |
|                      | 后置条件 |     查找是否存在相应的User，根据输入的用户id返回用户信息     |

| 需要的服务（需接口）               |                              |
| ---------------------------------- | ---------------------------- |
| 服务名                             | 服务                         |
| userMapper.selectByPhone(phone)    | 根据用户phone值查找用户      |
| userMapper.selectByPrimaryKey(uid) | 根据用户id查找用户信息       |
| userMapper.insert(user)            | 向数据库中插入新注册用户数据 |

**rechargebl模块**的接口规范如下表所示：

| 提供的服务（供接口） |          |                                                              |
| -------------------- | -------- | ------------------------------------------------------------ |
|                      | 语法     | ResultVO<UserVO> rechargeAccount(RechargeOrderVO rechargeOrderVO); |
| rechargeAccount      | 前置条件 | 充值数额符合输入规则                                         |
|                      | 后置条件 | 修改用户的余额                                               |

| 需要的服务（需接口）                      |              |
| ----------------------------------------- | ------------ |
| 服务名                                    | 服务         |
| userMapper.increaseBalance(userId, value) | 更新用户余额 |
| rechargeOrderVO.getUserId()               | 找到充值用户 |

**course_orderbl模块**的接口规范如下表所示：

| 提供的服务（供接口） |          |                                                              |
| -------------------- | -------- | ------------------------------------------------------------ |
|                      | 语法     | ResultVO<CourseOrderVO> insertCourseOrder(CourseOrderVO orderVO); |
| insertCourseOrder    | 前置条件 | 用户购买课程                                                 |
|                      | 后置条件 | 保存订单信息                                                 |
|                      |          |                                                              |
|                      | 语法     | ResultVO<CourseOrderVO> updateCourseOrder(Integer orderId, Integer orderStatus); |
| updateCourseOrder    | 前置条件 | 用户支付订单                                                 |
|                      | 后置条件 | 更新用户课程权限                                             |
|                      |          |                                                              |
|                      | 语法     | List<CourseOrderVO> getCourseOrders(Integer uid);            |
| getCourseOrders      | 前置条件 | 用户已经验证登录                                             |
|                      | 后置条件 | 返回用户订单列表                                             |

| 需要的服务（需接口）                                         |                  |
| ------------------------------------------------------------ | ---------------- |
| 服务名                                                       | 服务             |
| orderMapper.queryMostRecentOrder(orderVO.getUserId(), orderVO.getCourseId()) | 查询用户购买权限 |
| userMapper.selectByPrimaryKey(order.getUserId()              | 查找用户         |
| userMapper.decreaseBalance(user.getId(), order.getCost())    | 更新用户账户余额 |
| orderMapper.insert(order)                                    | 增加订单记录     |
| orderMapper.selectByPrimaryKey(orderId)                      | 查找订单         |
| orderMapper.updateByPrimaryKey(order)                        | 更新订单记录     |

**couse_warebl模块**的接口规范如下表所示：

| 提供的服务（供接口） |          |                                                              |
| -------------------- | -------- | ------------------------------------------------------------ |
|                      | 语法     | CourseWareVO getCourseWare(Integer uid, Integer courseWareId); |
| getCourseWare        | 前置条件 | 进入到网页，点击课件                                         |
|                      | 后置条件 | 返回课件信息                                                 |
|                      |          |                                                              |
|                      | 语法     | ResultVO<CourseWareVO> createCourseWare(CourseWareVO courseWareVO); |
| createCourseWare     | 前置条件 | 登录为教师用户                                               |
|                      | 后置条件 | 生成课件                                                     |
|                      |          |                                                              |
|                      | 语法     | ResultVO<CourseWareVO> updateCourseWare(CourseWareVO courseWareVO); |
| updateCourseWare     | 前置条件 | 登录为教师用户                                               |
|                      | 后置条件 | 更新课件                                                     |
|                      |          |                                                              |
|                      | 语法     | ResultVO<String> deleteCourseWare(Integer courseWareId);     |
| deleteCourseWare     | 前置条件 | 登录为教师用户                                               |
|                      | 后置条件 | 删除课件                                                     |

| 需要的服务（需接口）                                  |                      |
| ----------------------------------------------------- | -------------------- |
| 服务名                                                | 服务                 |
| courseWareMapper.selectByPrimaryKey(courseWareId)     | 查找课件             |
| courseOrderMapper.queryMostRecentOrder(uid, courseId) | 确认用户查看课件权限 |

**course_managebl模块**的接口规范如下表所示：

| 提供的服务（供接口） |          |                                                              |
| -------------------- | -------- | ------------------------------------------------------------ |
|                      | 语法     | ResultVO<CourseVO> createCourse(CourseVO courseVO);          |
| createCourse         | 前置条件 | 进入到网页，登录为教师用户                                   |
|                      | 后置条件 | 生成新课程                                                   |
|                      |          |                                                              |
|                      | 语法     | PageInfo<CourseVO> getCourses(Integer currPage, Integer pageSize, Integer uid, String key); |
| getCourses           | 前置条件 | 进入到网页，输入关键字                                       |
|                      | 后置条件 | 根据关键字分页返回课程信息                                   |
|                      |          |                                                              |
|                      | 语法     | CourseVO getCourse(Integer courseId, Integer uid)            |
| getCourse            | 前置条件 | 进入到网页，点击课程                                         |
|                      | 后置条件 | 返回课程信息                                                 |
|                      |          |                                                              |

| 需要的服务（需接口）                                    |                      |
| ------------------------------------------------------- | -------------------- |
| 服务名                                                  | 服务                 |
| courseMapper.queryAll(key)                              | 根据关键字查找课程   |
| courseMapper.selectByPrimaryKey(courseId)               | 查找课程             |
| courseMapper.selectByTeacherId(courseVO.getTeacherId()) | 查找教师所创建的课程 |

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

|          提供的服务（供接口）          |          |                                                              |
| :------------------------------------: | :------: | :----------------------------------------------------------: |
|                                        |   语法   |                  int insert(Course record);                  |
|          CourseMapper.insert           | 前置条件 |                     课程信息符合输入规则                     |
|                                        | 后置条件 |                    在数据库中添加课程信息                    |
|                                        |   语法   |             int deleteByPrimaryKey(Integer id);              |
|    CourseMapper.deleteByPrimaryKey     | 前置条件 |                       系统中存在该课程                       |
|                                        | 后置条件 |                        系统删除该课程                        |
|                                        |   语法   |            int updateByPrimaryKey(Course record);            |
|    CourseMapper.updateByPrimaryKey     | 前置条件 |                       系统中存在该课程                       |
|                                        | 后置条件 |                       系统更新课程信息                       |
|                                        |   语法   |                   int insert(User record);                   |
|           UserMapper.insert            | 前置条件 |                     用户数据符合输入规则                     |
|                                        | 后置条件 |                    在数据库中添加用户信息                    |
|                                        |   语法   | void increaseBalance(@Param(value = "id") Integer id, @Param(value = "delta")Integer delta); |
|       UserMapper.increaseBalance       | 前置条件 |                       余额符合输入规则                       |
|                                        | 后置条件 |                       修改用户账户余额                       |
|                                        |   语法   | CourseOrder queryMostRecentOrder(Integer userId, Integer courseId); |
| CourseOrderMapper.queryMostRecentOrder | 前置条件 |                  用户id、课程id符合输入规则                  |
|                                        | 后置条件 |                       返回课程查找结果                       |

