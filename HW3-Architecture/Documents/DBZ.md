## 1. 引言

### 1.1 编制目的

本软件体系结构描述文档对课程学习网站“Course Learning”进行了系统、详细的概要设计，主要目标是对该课程学习网站的详细设计和开发进行指导，并便于测试人员和用户进行沟通。

本文档面向开发人员、测试人员及最终用户编写，是相关人员了解“Course Learning”系统的导航。

### 1.2 词汇表

|    词汇名称     | 词汇含义 |        备注        |
| :-------------: | :------: | :----------------: |
| Course Learning | 课程学习 | 是该系统的英文名称 |

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

<img src="https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/%E9%80%BB%E8%BE%91%E8%AE%BE%E8%AE%A1%E6%96%B9%E6%A1%88%E5%8C%85%E5%9B%BE.png" style="zoom:50%;" />



## 6. 信息视角

### 6.1 数据持久化对象

系统的PO类就是对应相关的实体类，下面将对这些实体类作一些介绍。

- UserPO类包含用户的用户名、电话号码、密码、账户余额、用户角色、账号创建时间
- CoursePO类包含课程类型、课程简介、所属学校、创建/删除时间、课程价格、教师姓名
- CourseOrderPO类包含订单金额、课程名称、订单创建时间、支付状态
- CourseWarePO类包括课件题目、课件名称、上传时间、课件类型、课件大小
- RechargeOrderPO类包括充值金额、充值时间、充值用户
- PromotionPO类包括优惠时间、优惠额度、优惠适用课程

##### 下以持久化对象CoursePO的定义为例。

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

<img src="https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/数据库表.png" style="zoom: 67%;" />
