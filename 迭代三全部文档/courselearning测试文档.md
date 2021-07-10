# courselearning-测试文档

### 文档修改历史

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

1. **简介**

   1.1 项目背景

   1.2 测试目的

   1.3 测试环境

   1.4 测试范围

   1.5 参考资料

2. **测试计划**

   2.1 后端测试

   2.2 前端测试

3. **后端单元测试**

   3.1 测试方向

   3.2 测试准备

   3.3 测试用例

4. **后端集成测试**

   4.1 测试方向

   4.2 测试准备

   4.3 测试用例

5. **前端UI测试**

   5.1 测试方向

   5.2 测试准备

   5.3 测试用例

6. **e2e系统测试**

   6.1 测试方向

   6.2 测试准备

   6.3 测试用例

7. **测试覆盖率**

## 1. 简介

### 1.1 项目背景

+ 本项目是一个酒店预订系统，详细内容请参见需求用例文档，需求规格文档，体系结构文档，详细设计文档。

+ 本项目集成前端 + 后端，因此测试必须分别从两个方面着手。

### 1.2 测试目的

+ 前端页面渲染
+ 后端数据库交互
+ 后端接口完成度
+ 后端接口正确性
+ 后端接口之间的交互
+ 前端与后端的交互

### 1.3 测试环境

+ 后端运行于spring boot框架上，故后端测试采用Junit与Mockito和springbootTest进行单元测试与集成测试。

  + spring boot版本：v2.4.1
  + mybatis版本：v2.1.4
  
  + Junit版本：v4.13.2
  + Mockito版本：v2.23.4
+ 前端运行于vue-cli框架上，故前端测试采用jest测试。
  + vue-cli版本：v3
  + jest版本：v24.9.0
  + cypress版本：v4.9.0

### 1.4 测试范围

+ 测试主要为单元测试，前端目标是测试页面渲染测试，后端主要测试前端接口与数据库的交互性与正确性。

### 1.5 参考资料

+ 网上的Junit教程、Mockito教程。
+ 网上的jest教程

## 2. 测试计划

### 2.1 后端测试

1. **单元测试：**后端是根据前端的方法进行响应，所以主要测试地方为前端与后端接口的Controller包内的类与方法实现，目标进行单元测试，对每个方法进行调用，并进入数据库查找传入的资料或输出的资料并进行一一比对验证正确性。
2. **集成测试：**调用代码中与前端的接口controller，并对各个模块进行集成，测试代码模块之间的交互与正确性。

### 2.2 前端测试

1. **UI测试：**主要测试每个页面的渲染效果，利用Junit调用每一个页面并闯入必要的参数，测试HTML语言与CSS语言的正确性。
2. **e2e系统测试：**使用cypress编写自动化脚本并测试。

## 3. 后端单元测试

### 3.1 测试方向

+ 测试Controller类集合的每一个方法并调用Mapper类进行数据库验证。

### 3.2 测试准备

+ 重新运行sql文件确保数据库已经被初始化，不容易受外部数据干扰。
+ 关闭正在运行的后端避免测试途中外部传入新数据影响测试结果。

### 3.3 测试用例

#### 3.3.1 QuestionMapper Test

+ **测试前准备**
  
+ 初始化一个Question对象，随机输入数据，作为测试用的question。
  
+ **测试编号 B000000**
  
  1. 测试方法：QuestionMapper.insert
  
  2. 测试代码（截取）：
  
     ```java
     @Test
         public void testInsert(){
             Question question=new Question();
             question.setId(1);
             question.setCourseId(2);
             question.setTitle("水的化学式是多少？（直接输入即可，不用管下标）");
             question.setAnswer("H2O");
             question.setAnalysis("水的化学式就是H2O");
             question.setCreateTime(new Date());
             questionMapper.insert(question);
             Question assertQuestion=questionMapper.selectByTitle(question.getTitle());
             assert assertQuestion.getAnalysis().equals("水的化学式就是H2O");
         }
     ```
  
+ **测试编号 B000001**

  1.测试方法：QuestionMapper.selectBycourseID

  2.测试代码（截取）：

```java
@Test
    public void testQueryByCourseId1(){
        //教师查询题库的方法单元测试1.数据表中有该题库的题目时
        Question question1=new Question();
        question1.setId(2);
        question1.setCourseId(2);
        question1.setTitle("水的化学式是多少？（直接输入即可，不用管下标）.");
        question1.setAnswer("H2O");
        question1.setAnalysis("水的化学式就是H2O");
        question1.setCreateTime(new Date());
        Question question2=new Question();
        question2.setId(3);
        question2.setCourseId(2);
        question2.setTitle("水的化学式是多少？（直接输入即可，不用管下标）..");
        question2.setAnswer("H2O");
        question2.setAnalysis("水的化学式就是H2O");
        question2.setCreateTime(new Date());
        Question question3=new Question();
        question3.setId(4);
        question3.setCourseId(2);
        question3.setTitle("水的化学式是多少？（直接输入即可，不用管下标）...");
        question3.setAnswer("H2O");
        question3.setAnalysis("水的化学式就是H2O");
        question3.setCreateTime(new Date());
        questionMapper.insert(question1);
        questionMapper.insert(question2);
        questionMapper.insert(question3);
        List<Question> correct=new ArrayList<>();
        correct.add(question1);
        correct.add(question2);
        correct.add(question3);
        List<Question> queryResult=questionMapper.selectBycourseID(2);
        assert correct.size()==queryResult.size();
        for(int i=0;i<3;i++){
            assert correct.get(i).getTitle().equals(queryResult.get(i).getTitle());
        }
    }
```

+ **测试编号 B000002**

  1.测试方法：QuestionMapper.selectBycourseID

  2.测试代码（截取）：

```java
@Test
    public void testQueryByCourseId2(){
        //教师查询题库的方法单元测试用例2.数据表中没有该题库的题目时
        List<Question> queryResult=questionMapper.selectBycourseID(5);
        assert queryResult.size()==0;
    }
```

+ **测试结果**

运行通过

#### 3.3.2  ExamMapper Test

#### 3.3.3  ExamService Test

#### 3.3.4  ExamInfoMapper Test

#### 3.3.5  AnswerMapper Test

#### 3.3.6  ScoreMapper Test

#### 3.3.7  VipOrderMapper Test

上面的几个我列出来的单元测试和两个集成测试你们都加上吧，仿照我写的第一个写，我心脏疼，肝不动了

## 4. 后端集成测试

### 4.1 测试方向

+ 测试各个用例对应逻辑层集成之后交互的情况，并验证正确性。

### 4.2 测试准备

+ 重新运行sql文件确保数据库已经被初始化，不容易受外部数据干扰。
+ 关闭正在运行的后端避免测试途中外部传入新数据影响测试结果。

### 4.3 测试用例

#### 4.3.1 ？？？ Test

+ **测试前准备**

  + 初始化一个？？？类，随机输入数据，作为测试用的？？？。

+ **测试编号 B000038**

  1. 测试方法：
  2. 集成模块：questionService.

+ **测试结果**

  

## 5. 前端集成测试部分

| 测试时间        | 测试内容                       | 测试人 | 测试工具 |
| --------------- | ------------------------------ | ------ | -------- |
| 2021/7/9 13:43  | 教师向某课程题库中添加题目     | 丁炳智 | Postman  |
| 2021/7/9 14:30  | 教师获取课程题库               | 丁炳智 | Postman  |
| 2021/7/10 23:00 | 学生开通VIP会员                | 丁炳智 | Postman  |
| 2021/7/10 23:37 | 教师发布测试卷                 | 丁炳智 | Postman  |
| 2021/7/10 23:55 | 学生获取测试列表               | 丁炳智 | Postman  |
| 2021/7/11 00:17 | 学生获取测试题目               | 丁炳智 | Postman  |
| 2021/7/11 00:38 | 学生提交测试答案               | 丁炳智 | Postman  |
| 2021/7/11 01:07 | 学生获取已完成测试列表         | 丁炳智 | Postman  |
| 2021/7/11 01:32 | 学生获取某一已完成测试答题情况 | 丁炳智 | Postman  |

### 一、教师向某课程题库中添加题目

HTTP REST请求：POST，参数类型：Payload（JSON）

接口：<code>/api/question/add_question</code>

#### 测试用例：

```json
[
	{
		"analysis": "艺术",
		"answer": "贝多芬",
		"courseId": "1",
		"title": "月光奏鸣曲是谁创作的？"
	},
    {
		"analysis": "美食",
		"answer": "肯德基",
		"courseId": "1",
		"title": "KFC的中文名是什么？"
	},
    {
		"analysis": "这道题需要用不定积分进行求解",
		"answer": "x^2/3 + C",
		"courseId": "1",
		"title": "求∫x^2dx"
	},
    {
		"analysis": "软件工程基本概念之一",
		"answer": "增量迭代模型",
		"courseId": "1",
		"title": "Courselearning网站开发采用了什么模型？"
	},
    {
		"analysis": "数学基本概念之一",
		"answer": "交",
		"courseId": "1",
		"title": "如何求两个集合的公共部分？"
	},
    {
		"analysis": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
		"answer": "yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
		"courseId": "1",
		"title": "zzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz"
	}
]
```

#### 测试脚本：

- 输入：题目JSON串，包含题目的答案、解析、标题，以及题目所属课程的ID

- 期望返回：JSON对象，其中code对象值为1，msg对象值为”题目添加成功！“

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210709135006850.png" alt="image-20210709135006850" style="zoom:67%;" />

```js
pm.test("添加题库测试", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.code).to.eql(1);
    pm.expect(jsonData.msg).to.eql("题目添加成功！");
});
```

#### 自动化测试运行结果：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210709135122210.png" alt="image-20210709135122210" style="zoom:67%;" />

#### 实际返回数据（仅举一例）：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210709141424777.png" alt="image-20210709141424777" style="zoom:67%;" />

#### 检查数据库：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210709135851389.png" alt="image-20210709135851389" style="zoom:67%;" />

自动化测试完毕。



### 二、教师获取课程题库

HTTP REST请求：GET，参数类型：Integer（courseID）

接口：<code>/api/question/{courseID}</code>

#### 测试脚本：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210709140509924.png" alt="image-20210709140509924" style="zoom:67%;" />

- 输入：课程的ID

- 期望：返回课程的题目数组，响应时间不超过200ms

```js
pm.test("Response time is less than 200ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(200);
});
```

#### 自动化测试运行结果：

![image-20210709140745366](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210709140745366.png)

#### 实际返回数据：

##### 以课程1为例：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210709140923892.png" alt="image-20210709140923892" style="zoom:67%;" />

实际测试时，课程1和课程2的题干相同，但返回的数据中，courseId不同，说明确实返回了对应课程的题目列表。

自动化测试完毕。



### 三、开通会员

HTTP REST请求：POST，参数类型：Integer（uid）

接口：<code>/api/vip/{uid}</code>

#### 测试脚本：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210710224342004.png" alt="image-20210710224342004" style="zoom:67%;" />

- 输入：uid

- 期望：返回会员开通成功信息

```js
pm.test("会员开通测试", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.code).to.eql(1);
    pm.expect(jsonData.msg).to.eql("开通会员成功!");
    pm.expect(jsonData.data._vip).to.eql(true);
    pm.expect(jsonData.data.userRole).to.eql("STUDENT");
});
```

#### 自动化测试运行结果：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210710231735431.png" alt="image-20210710231735431" style="zoom:67%;" />

#### 实际返回数据（仅举一例uid=2时）：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210710224626130.png" alt="image-20210710224626130" style="zoom:67%;" />

自动化测试完毕。



### 四、教师发布测试

HTTP REST请求：POST，参数类型：Payload

接口：<code>/api/exam/release</code>

#### 测试脚本：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210710233348366.png" alt="image-20210710233348366" style="zoom:67%;" />

- 输入：Payload（JSON对象），例如：

```json
{
    courseId: 1,
	endTime: "2021-07-16 23:00:00",
	questions: [
    	{
            analysis: "软件工程基本概念",
			answer: "软件工程是运用系统的、可量化的方法进行软件开发、运营和维护。",
			courseId: 1,
			createTime: "2021-07-10 23:22:29",
			id: 1,
			title: "软件工程的定义？"
        },
        {
            analysis: "基本素养",
			answer: "刘钦",
			courseId: 1,
			createTime: "2021-07-10 23:23:04",
			id: 2,
			title: "软件工程这门课的教师是谁？"
        },
        {
            analysis: "行业发展",
			answer: "有",
			courseId: 1,
			createTime: "2021-07-10 23:23:23",
			id: 3,
			title: "软件工程有前景吗？"
        }
    ],
	startTime: "2021-07-10 23:00:00",
	title: "软件工程1课程测试"
}
```

- 期望：返回测试发布成功相关数据

#### 自动化测试运行结果：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210710233327817.png" alt="image-20210710233327817" style="zoom:67%;" />

#### 实际返回数据：

##### 以发布的其中一项测试为例：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210710233418205.png" alt="image-20210710233418205" style="zoom:67%;" />

自动化测试完毕。



### 五、学生获取测试列表

HTTP REST请求：GET，参数类型：Integer（courseID）

接口：<code>/api/exam/get/{courseID}</code>

#### 测试脚本：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210710234708265.png" alt="image-20210710234708265" style="zoom:67%;" />

- 输入：courseID

- 期望：返回该课程所有测试，每次响应不超过550ms

#### 自动化测试运行结果：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210710234209361.png" alt="image-20210710234209361" style="zoom:67%;" />

#### 实际返回数据：

##### 以其中一次请求为例：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210710234407451.png" alt="image-20210710234407451" style="zoom:67%;" />

#### 数据库中该课程已有测试为：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210710234435833.png" alt="image-20210710234435833" style="zoom:67%;" />

请求成功，自动化测试完毕。



### 六、学生获取测试题目

HTTP REST请求：GET，参数类型：Integer（examID）

接口：<code>/api/exam/getQuestions/{examID}</code>

#### 测试脚本：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210710235052483.png" alt="image-20210710235052483" style="zoom:67%;" />

- 输入：examID

- 期望：返回该场考试所有题目

#### 自动化测试运行结果：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210710235029425.png" alt="image-20210710235029425" style="zoom:67%;" />

#### 实际返回数据：

##### 以其中一次请求为例：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210710235121758.png" alt="image-20210710235121758" style="zoom:67%;" />

请求成功，自动化测试完毕。



### 七、学生提交测试答案

HTTP REST请求：POST，参数类型：Payload

接口：<code>/api/exam/submit</code>

#### 测试脚本：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210711000718338.png" alt="image-20210711000718338" style="zoom:67%;" />

- 输入：JSON对象，例如：

```json
{
    "answers": [
        {
            "Id": -1,
            "answer": "1",
            "examId": 1,
            "isCorrect": false,
            "questionId": 1,
            "uid": 2
        },
        {
            "Id": -1,
            "answer": "1",
            "examId": 1,
            "isCorrect": false,
            "questionId": 2,
            "uid": 2
        },
        {
            "Id": -1,
            "answer": "1",
            "examId": 1,
            "isCorrect": false,
            "questionId": 3,
            "uid": 2
        }
    ],
    "examID": 2,
    "uid": 2
}
```

- 期望：返回考试提交成功信息

#### 自动化测试运行结果：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210711000704434.png" alt="image-20210711000704434" style="zoom:67%;" />

#### 实际返回数据：

##### 以其中一次请求为例：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210711000425711.png" alt="image-20210711000425711" style="zoom:67%;" />

请求成功，自动化测试完毕。



### 八、学生获取已完成测试列表

HTTP REST请求：GET，参数类型：Integer（uid）

接口：<code>/api/exam/{uid}</code>

#### 测试脚本：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210711002239197.png" alt="image-20210711002239197" style="zoom:67%;" />

- 输入：uid

- 期望：返回id为uid的学生已完成的所有测试，每次响应不超过550ms

#### 自动化测试运行结果：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210711002217029.png" alt="image-20210711002217029" style="zoom:67%;" />

#### 实际返回数据：

##### 以其中一次请求为例：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210711002312357.png" alt="image-20210711002312357" style="zoom:67%;" />

请求成功，自动化测试完毕。



### 九、 学生获取某一已完成测试答题情况

HTTP REST请求：GET，参数类型：Integer（uid、examID）

接口：<code>/api/exam/getResult/{uid}?exam_id={exam_id}</code>

#### 测试脚本：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210711002804578.png" alt="image-20210711002804578" style="zoom:67%;" />

- 输入：uid、exam_id

- 期望：返回学生已完成的exam_id次测试的答题状况，每次响应不超过550ms

#### 自动化测试运行结果：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210711002845364.png" alt="image-20210711002845364" style="zoom:67%;" />

#### 实际返回数据：

##### 以其中一次请求为例：

<img src="https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/image-20210711002908653.png" alt="image-20210711002908653" style="zoom:67%;" />

请求成功，自动化测试完毕。

## 7. 测试覆盖率

后端集成测试覆盖7个用例，用例总数为8，覆盖率为87.5%

前端单元测试覆盖率100%
