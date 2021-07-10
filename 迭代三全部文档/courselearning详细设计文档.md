# courselearning—详细设计文档

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



## 1、引言

### 1.1、编制目的

本报告详细完成对course learning课程学习网站迭代三的详细设计，达到指导后续软件构造的目的，同时实现和测试人员及用户的沟通。

本报告面向开发人员、测试人员及最终用户编写，是了解系统的导航。

### 1.2、词汇表

| 词汇名称 | 词汇含义                                | 备注   |
| -------- | --------------------------------------- | ------ |
| CSW      | 即course learning website，课程学习网站 | ...... |
| ......   | ......                                  | ...... |


### 1.3、参考资料


## 2、产品概述

参考course learning课程学习网站用例文档和course learning课程学习网站软件需求规格说明文档中对产品的概括描述

## 3、体系结构设计概述

参考course learning课程学习网站体系结构文档中对体系结构设计的概述

## 4、结构视角

结构视角由于持久层是自动生成，展示层关注UI设计并不需要详细设计支撑，我们只关注业务逻辑层的分解设计。

### 4.1、业务逻辑层的分解

### 4.1.1、vip模块
#### （1）模块概述

vip模块位于每一层的order包内部。

vip模块承担的需求参见需求规格说明文档功能需求及相关非功能需求。

vip模块的职责及接口参见软件体系结构文档。

#### （2）整体结构

根据体系结构设计，我们将系统分为展示层、业务逻辑层和数据层。该模块内部分为控制层、逻辑服务层，这两层之间为了增加灵活性，我们会添加接口，控制层和逻辑服务层之间添加了service.VipService接口。此外业务逻辑层和数据层之间添加了mapperservice.VipMapper接口。为了隔离业务逻辑职责和逻辑控制职责，我们增加了VipController，这样VipContoller会对Vip相关的业务逻辑处理委托给VipService对象。User是作为用户记录的持久化对象被添加到设计模型中去的，其中存储了用户vip相关的信息。UserVO是作为用户记录的业务数据对象被添加到设计模型中去的，其中暂时存储用户vip相关信息。

vip模块的设计如图所示：

![vip模块各个类的设计](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/vip%E6%A8%A1%E5%9D%97%E5%90%84%E4%B8%AA%E7%B1%BB%E7%9A%84%E8%AE%BE%E8%AE%A1.jpg)

vip模块各个类的职责如表所示：

| 类             | 职责                                                         |
| -------------- | ------------------------------------------------------------ |
| VipController  | 负责通过VipService接口控制业务逻辑方法的寻星，隔离业务逻辑职责和逻辑控制职责 |
| VipServiceImpl | 负责实现充值成为Vip的业务逻辑                                |
| UserVO         | 控制暂时存储数剧的用户业务对象                               |
| User           | 控制存储用户对象的持久数据                                   |

#### （3）模块内部类的接口规范

VipController和VipServiceImpl的接口规范如下两表所示：

1、VipController接口规范

<table>
	<tr>
	    <td colspan="3">提供的服务(供接口)</th>  
	</tr >
	<tr >
	    <td rowspan="3">VipController.openVip</td>
	    <td>语法</td>
	    <td>public Result&#60UserVO&#62 openVip(@PathVariable Integer uid)</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>前端调用了api.vip.openVip，并传给后端类型为Integer的uid</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>调用Springboot配置实例化的VipService对象的openVip方法</td>
	</tr>
</table>

<table>
	<tr>
	    <td colspan="3">需要的服务(需接口)</th>  
	</tr >
	<tr >
	    <td>VipService.openVip(Integer uid)</td>
	    <td>为用户id为uid的用户开通会员服务</td>
	</tr>
</table>

2、VipServiceImpl接口规范

<table>
	<tr>
	    <td colspan="3">提供的服务(供接口)</th>  
	</tr >
	<tr >
	    <td rowspan="3">VipServiceImpl.openVip</td>
	    <td>语法</td>
	    <td>public Result&#60UserVO&#62 openVip(Integer uid)</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>学生用户使用开通会员服务</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>为用户id为uid的用户开通会员服务</td>
	</tr>
</table>

<table>
	<tr>
	    <td colspan="2">需要的服务(需接口)</th>  
	</tr >
	<tr >
	    <td>VipMapper.openVip(Integer uid)</td>
	    <td>根据uid查找单一持久化对象并修改其中的is_vip字段</td>
	</tr>
</table>


#### （4）业务逻辑层动态模型

下图表明在courselearning课程学习网站中，当用户点击开通会员并支付后，vip业务逻辑处理的相关对象之间的协作。

![开通Vip顺序图](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/%E5%BC%80%E9%80%9AVip%E9%A1%BA%E5%BA%8F%E5%9B%BE.jpg)

#### （5）业务逻辑层的设计原理

利用委托式控制风格，每个界面需要访问的业务逻辑有各自的控制器委托给不同的业务逻辑对象。

### 4.1.2、question模块

#### （1）模块概述

question模块位于每一层的exam包内部。

question模块承担的需求参见需求规格说明文档功能需求及相关非功能需求。

question模块的职责及接口参见软件体系结构文档。

#### （2）整体结构

根据体系结构设计，我们将系统分为展示层、业务逻辑层和数据层。该模块内部分为控制层、逻辑服务层，这两层之间为了增加灵活性，我们会添加接口，控制层和逻辑服务层之间添加了service.QuestionService接口。此外业务逻辑层和数据层之间添加了mapperservice.QuestionMapper接口。为了隔离业务逻辑职责和逻辑控制职责，我们增加了QuestionController，这样QuestionContoller会对测试中的题目相关的业务逻辑处理委托给QuestionService对象。Question是作为用户记录的持久化对象被添加到设计模型中去的，其中存储了题目question相关的信息。QuestionVO是作为题目记录的业务数据对象被添加到设计模型中去的，其中暂时存储业务题目Question相关信息。

Question模块的设计如图所示：

![question模块各个类的设计](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/question%E6%A8%A1%E5%9D%97%E5%90%84%E4%B8%AA%E7%B1%BB%E7%9A%84%E8%AE%BE%E8%AE%A1.jpg)

Question模块各个类的职责如表所示：

| 类                  | 职责                                                         |
| ------------------- | ------------------------------------------------------------ |
| QuestionController  | 负责通过QuestionService接口控制业务逻辑方法的调用，隔离业务逻辑职责和逻辑控制职责 |
| QuestionServiceImpl | 负责实现上传题目和根据课程返回课程的题库两个功能点成为Question的业务逻辑 |
| QuestionVO          | 控制暂时存储数据的题目业务对象                               |
| Question            | 控制存储题目对象的持久数据                                   |

#### （3）模块内部类的接口规范

QuestionController和QuestionServiceImpl的接口规范如下两表所示：

1、QuestionController接口规范

<table>
	<tr>
	    <td colspan="3">提供的服务(供接口)</th>  
	</tr >
	<tr >
	    <td rowspan="3">QuestionController.addQuestionC</td>
	    <td>语法</td>
	    <td>public Result&#60QuestionVO&#62 addQuestionC(@RequestBody QuestionVO question)</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>前端调用了api.question.addQuestion，并传给后端类型为QuestionVo的question业务对象</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>调用通过Springboot配置实例化的QuestionService对象的addQuestion方法</td>
	</tr>
<tr >
	    <td rowspan="3">QuestionController.getQuestionsByCourseID</td>
	    <td>语法</td>
	    <td>public Result&#60QuestionVO&#62 getQuestionsByCourseID(@PathVariable Integer courseID)</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>前端调用了api.question.getQuestionsByCourseID，并传给后端类型为Integer的courseID</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>调用通过Springboot配置实例化的QuestionService对象的getQuestionsByCourseID方法</td>
	</tr>
</table>

<table>
	<tr>
	    <td colspan="2">需要的服务(需接口)</th>  
	</tr >
<tr >
	    <td>服务名</td>
	    <td>服务</td>
	</tr>
<tr >
	    <td>QuestionService.addQuestion(QuestionVO question)</td>
	    <td>向该课程题库里添加前端传来的一个问题</td>
	</tr>
	<tr >
	    <td>QuestionService.getQuestionsByCourseID(Integer courseId)</td>
	    <td>查找并返回对应courseID的题库里包含的问题</td>
	</tr>
</table>

2、QuestionServiceImpl接口规范

<table>
	<tr>
	    <td colspan="3">提供的服务(供接口)</th>  
	</tr >
	<tr >
	    <td rowspan="3">QuestionServiceImpl.addQuestion</td>
	    <td>语法</td>
	    <td>public Result&#60QuestionVO&#62 addQuestion(QuestionVO question)</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>教师用户启动一个向某一课程题库添加题目回合</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>在一个添加题目回合中，增加对应课程题库的题目记录</td>
	</tr>
<tr >
	    <td rowspan="3">QuestionServiceImpl.getQuestionsByCourseID</td>
	    <td>语法</td>
	    <td>public Result&#60QuestionVO&#62 getQuestionsByCourseID(Integer courseID)</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>教师用户在向创建的测试之前添加题目前启动查询该课程的题库</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>返回该课程对应题目的题库</td>
	</tr>
</table>

<table>
	<tr>
	    <td colspan="2">需要的服务(需接口)</th>  
	</tr >
<tr >
	    <td>服务名</td>
	    <td>服务</td>
	</tr>
<tr >
	    <td>QuestionMapper.insert(Question question)</td>
	    <td>插入单一持久化对象</td>
	</tr>
	<tr >
	    <td>QuestionMapper.selectBycourseID(Integer courseId)</td>
	    <td>根据courseId进行查找多个持久化对象</td>
	</tr>
</table>

#### （4）业务逻辑层动态模型

1、下图表明在courselearning课程学习网站中，当用户向题库中添加题目后，question业务逻辑处理的相关对象之间的协作。

![向题库中添加题目的顺序图](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/%E5%90%91%E9%A2%98%E5%BA%93%E4%B8%AD%E6%B7%BB%E5%8A%A0%E9%A2%98%E7%9B%AE%E7%9A%84%E9%A1%BA%E5%BA%8F%E5%9B%BE.jpg)

2、下图表明在courselearning课程学习网站中，当用户开始从题库中选择题目前，需要请求题库中的全部题目，question业务逻辑处理的相关对象之间的协作。

![得到题库中所有题目的顺序图](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/%E5%BE%97%E5%88%B0%E9%A2%98%E5%BA%93%E4%B8%AD%E6%89%80%E6%9C%89%E9%A2%98%E7%9B%AE%E7%9A%84%E9%A1%BA%E5%BA%8F%E5%9B%BE.jpg)

#### （5）业务逻辑层的设计原理

利用委托式控制风格，每个界面需要访问的业务逻辑有各自的控制器委托给不同的业务逻辑对象。

### 4.1.1、exam模块

#### （1）模块概述

exam模块位于每一层的exam包内部。

exam模块承担的需求参见需求规格说明文档功能需求及相关非功能需求。

exam模块的职责及接口参见软件体系结构文档。

#### （2）整体结构

根据体系结构设计，我们将系统分为展示层、业务逻辑层和数据层。该模块内部分为控制层、逻辑服务层，这两层之间为了增加灵活性，我们会添加接口，控制层和逻辑服务层之间添加了service.ExamService接口。此外业务逻辑层和数据层之间添加了mapperservice.ExamMapper接口。为了隔离业务逻辑职责和逻辑控制职责，我们增加了ExamController，这样ExamContoller会对测试exam相关的业务逻辑处理委托给ExamService对象。Exam是作为测试基本信息记录的持久化对象被添加到设计模型中去的，其中存储了测试exam相关的信息。ExamVO是作为测试基本信息记录的业务数据对象被添加到设计模型中去的，其中暂时存储测试exam相关信息。ExamInfo是作为测试“题目ID-课程ID”对记录的持久化对象被添加到设计模型中去的，其中存储了测试卷题目的相关的信息。ExamInfoVO是作为测试“题目ID-课程ID”对记录的业务数据对象被添加到设计模型中去的，其中暂时存储测试卷题目相关信息。Answer是作为学生测试答案记录的持久化对象被添加到设计模型中去的，其中存储了学生答题答案answer相关的信息。AnswerVO是作为学生测试答案记录的业务数据对象被添加到设计模型中去的，其中暂时存储学生答题答案answer相关信息。Score是作为学生测试得分记录的持久化对象被添加到设计模型中去的，其中存储了得分score相关的信息。ScoreVO是作为学生测试得分记录的业务数据对象被添加到设计模型中去的，其中暂时存储得分score相关信息。

exam模块的设计如图所示：

![exam模块各个类的设计](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/exam%E6%A8%A1%E5%9D%97%E5%90%84%E4%B8%AA%E7%B1%BB%E7%9A%84%E8%AE%BE%E8%AE%A1.jpg)

exam模块各个类的职责如表所示：

| 类              | 职责                                                         |
| --------------- | ------------------------------------------------------------ |
| examController  | 负责通过ExamService接口控制业务逻辑方法的调用，隔离业务逻辑职责和逻辑控制职责 |
| examServiceImpl | 负责实现发布测试卷（教师）、获取考试列表（学生），学生提交考试结果、学生获取已做试卷列表、获取考试结果等五个用例成为exam模块的业务逻辑实现 |
| ExamVO          | 控制暂时存储数据的测试业务对象                               |
| Exam            | 控制存储测试对象的持久数据                                   |
| ExamInfoVO      | 控制暂时存储数据的测试题目业务对象                           |
| ExamInfo        | 控制存储测试题目对象的持久数据                               |
| AnswerVO        | 控制暂时存储数据的答案业务对象                               |
| Answer          | 控制存储答案对象的持久数据                                   |
| ScoreVO         | 控制暂时存储数据的得分业务对象                               |
| Score           | 控制存储得分对象的持久数据                                   |

#### （3）模块内部类的接口规范

ExamController和ExamService的接口规范如下两表所示：

1、ExamController接口规范

<table>
	<tr>
	    <td colspan="3">提供的服务(供接口)</th>  
	</tr >
	<tr >
	    <td rowspan="3">ExamController.releaseC</td>
	    <td>语法</td>
	    <td>public Result&#60ExamVO&#62 releaseC(@RequestBody String jsonStr)</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>前端调用了api.exam.releaseExam，并传给后端类型为String的json串</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>处理了json串并调用Springboot配置实例化的ExamService对象的release方法</td>
	</tr>
<tr >
	    <td rowspan="3">ExamController.getHasDoneExam</td>
	    <td>语法</td>
	    <td>public Result&#60ExamVO&#62 getHasDoneExam(@PathVariable Integer uid)</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>前端调用了api.exam.getExamsByUserID，并传给后端类型为Integer的uid</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>调用Springboot配置实例化的ExamService对象的getHasDoneExam方法</td>
	</tr>
<tr >
	    <td rowspan="3">ExamController.getExamResult</td>
	    <td>语法</td>
	    <td>public ExamReviewVO getExamResult(@PathVariable Integer uid, @RequestParam Integer exam_id)</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>前端调用了api.exam.getExamResults，并传给后端类型为Integer的uid和exam_id</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>调用Springboot配置实例化的ExamService对象的getExamResult方法</td>
	</tr>
<tr >
	    <td rowspan="3">ExamController.getExamsByCourseIDC</td>
	    <td>语法</td>
	    <td>public List&#60ExamVO&#62 getExamsByCourseIDC(@PathVariable Integer courseID)</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>前端调用了api.exam.getExamsByCourseId，并传给后端类型为Integer的courseID</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>调用Springboot配置实例化的ExamService对象的getExamsByCourseId方法</td>
	</tr>
<tr >
	    <td rowspan="3">ExamController.submitAnswers</td>
	    <td>语法</td>
	    <td>public Result&#60List&#60AnswerVO&#62&#62 submitAnswers(@RequestBody String jsonStr)</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>前端调用了api.exam.submitExam，并传给后端类型为String的json串/td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>处理了json串并调用Springboot配置实例化的ExamService对象的insertAnswers方法</td>
	</tr>
</table>

<table>
	<tr>
	    <td colspan="3">需要的服务(需接口)</th>  
	</tr >
	<tr >
	    <td>服务名</td>
	    <td>服务</td>
	</tr>
<tr >
	    <td>ExamService.release(ExamVO examVO)</td>
	    <td>发布一个测试</td>
	</tr>
<tr >
	    <td>ExamService.getHasDoneExam(Integer uid)</td>
	    <td>获得完成的测试列表</td>
	</tr>
<tr >
	    <td>ExamService.getExamResult(Integer uid, Integer exam_id)</td>
	    <td>获得测试结果</td>
	</tr>
<tr >
	    <td>ExamService.getExamsByCourseId(Integer courseId)</td>
	    <td>获得某一课程的全部测试</td>
	</tr>
<tr >
	    <td>ExamService.insertAnswers(AnswerListVO answerListVO)</td>
	    <td>完成学生答案录入并计算得分</td>
	</tr>
</table>

2、ExamServiceImpl接口规范

<table>
	<tr>
	    <td colspan="3">提供的服务(供接口)</th>  
	</tr >
	<tr >
	    <td rowspan="3">ExamServiceImpl.release</td>
	    <td>语法</td>
	    <td>public ResultVO&#60ExamVO&#62 release(ExamVO examVO)</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>启动一个发布测试回合</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>在一个发布测试回合中，增加属于某一课程的测试信息</td>
	</tr>
<tr >
	    <td rowspan="3">ExamServiceImpl.getHasDoneExam</td>
	    <td>语法</td>
	    <td>public List&#60ExamVO&#62 getHasDoneExam(Integer uid)</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>学生用户请求查找已经做过的测试</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>返回此学生用户已经做过测试的基本信息</td>
	</tr>
<tr >
	    <td rowspan="3">ExamServiceImpl.getExamResult</td>
	    <td>语法</td>
	    <td>public ExamReviewVO getExamResult(Integer uid, Integer exam_id)</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>学生用户请求获得某一测试的测试得分</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>返回该测试该学生用户的结果及得分情况</td>
	</tr>
<tr >
	    <td rowspan="3">ExamServiceImpl.getExamsByCourseId</td>
	    <td>语法</td>
	    <td>public List&#60ExamVO&#62 getExamsByCourseId(Integer courseId)</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>学生用户请求获得某一课程的全部测试信息</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>返回某一课程的全部测试信息</td>
	</tr>
<tr >
	    <td rowspan="3">ExamServiceImpl.insertAnswers</td>
	    <td>语法</td>
	    <td>public ResultVO&#60List&#60AnswerVO&#62&#62 insertAnswers(AnswerListVO answerListVO)</td>
	</tr>
	<tr>
	    <td>前置条件</td>
	    <td>启动一个“学生用户完成某一测试并提交答案”回合</td>
	</tr>
	<tr>
	    <td>后置条件</td>
	    <td>在一个“学生用户完成某一测试并提交答案”回合中，增加该学生参加某一测试所填写答案的信息，并增加该学生参加某一测试的得分信息</td>
	</tr>
</table>

<table>
	<tr>
	    <td colspan="3">需要的服务(需接口),顺序为逻辑处理层ServiceImpl调用需接口的顺序</th>  
	</tr >
	<tr >
	    <td>服务名</td>
	    <td>服务</td>
	</tr>
<tr >
	    <td>ExamMapper.selectByTitle(String tltle)</td>
	    <td>根据ID查找单一持久化对象</td>
	</tr>
<tr >
	    <td>ExamMapper.selectByTitleAndCourseId(String tltle,int CourseId)</td>
	    <td>根据ID查找单一持久化对象</td>
	</tr>
<tr >
	    <td>ExamInfoMapper.insert(ExamInfo examInfo)</td>
	    <td>插入单一持久化对象</td>
	</tr>
<tr >
	    <td>ScoreMapper.selectHasDoneExamsIdByUid(int uid)</td>
	    <td>根据ID查找多个持久化对象</td>
	</tr>
<tr >
	    <td>ExamMapper.selectByPrimaryKey(int id)</td>
	    <td>根据ID查找单一持久化对象</td>
	</tr>
<tr >
	    <td>ScoreMapper.selectScore(int uid,int exam_id)</td>
	    <td>根据ID查找单一持久化对象</td>
	</tr>
<tr >
	    <td>AnswerMapper.getQuestionIds(int uid,int exam_id)</td>
	    <td>根据ID查找多个持久化对象</td>
	</tr>
<tr >
	    <td>QuestionMapper.selectByPrimaryKey(int id)</td>
	    <td>根据ID查找单一持久化对象</td>
	</tr>
<tr >
	    <td>AnswerMapper.getAnswerByUidAndQuestionIdAndExamId(int uid, int question_id, int exam_id)</td>
	    <td>根据ID查找单一持久化对象</td>
	</tr>
<tr >
	    <td>ExamMapper.selectByCourseId(int cid)</td>
	    <td>根据ID查找多个持久化对象</td>
	</tr>
<tr >
	    <td>AnswerMapper.insert(Answer answer)</td>
	    <td>插入单一持久化对象</td>
	</tr>
<tr >
	    <td>ScoreMapper.insert(Score score)</td>
	    <td>插入单一持久化对象</td>
	</tr>
</table>


#### （4）业务逻辑层动态模型

1、下图表明在courselearning课程学习网站中，当教师用户点击发布测试后，exam业务逻辑处理的相关对象之间的协作。

![教师发布测试的顺序图](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/%E6%95%99%E5%B8%88%E5%8F%91%E5%B8%83%E6%B5%8B%E8%AF%95%E7%9A%84%E9%A1%BA%E5%BA%8F%E5%9B%BE.jpg)

2、下图表明在courselearning课程学习网站中，当学生用户点击查看已完成测试后，exam模块业务逻辑处理的相关对象之间的协作。

![学生查找已做测试的顺序图](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/%E5%AD%A6%E7%94%9F%E6%9F%A5%E6%89%BE%E5%B7%B2%E5%81%9A%E6%B5%8B%E8%AF%95%E7%9A%84%E9%A1%BA%E5%BA%8F%E5%9B%BE.jpg)

3、下图表明在courselearning课程学习网站中，当学生用户选择查看某一完成测试结果后，exam模块业务逻辑处理的相关对象之间的协作。

![学生获得某一测试的结果的顺序图](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/%E5%AD%A6%E7%94%9F%E8%8E%B7%E5%BE%97%E6%9F%90%E4%B8%80%E6%B5%8B%E8%AF%95%E7%9A%84%E7%BB%93%E6%9E%9C%E7%9A%84%E9%A1%BA%E5%BA%8F%E5%9B%BE.jpg)

4、下图表明在courselearning课程学习网站中，当学生用户点击参加课程测试前，需要请求该课程的全部测试，exam模块业务逻辑处理的相关对象之间的协作。

![学生获得某一课程全部测试的顺序图](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/%E5%AD%A6%E7%94%9F%E8%8E%B7%E5%BE%97%E6%9F%90%E4%B8%80%E8%AF%BE%E7%A8%8B%E5%85%A8%E9%83%A8%E6%B5%8B%E8%AF%95%E7%9A%84%E9%A1%BA%E5%BA%8F%E5%9B%BE.jpg)

5、下图表明在courselearning课程学习网站中，当学生用户选择某一测试参加并提交答卷后，exam模块业务逻辑处理的相关对象之间的协作。

![学生提交答案的顺序图](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/%E5%AD%A6%E7%94%9F%E6%8F%90%E4%BA%A4%E7%AD%94%E6%A1%88%E7%9A%84%E9%A1%BA%E5%BA%8F%E5%9B%BE.jpg)

#### （5）业务逻辑层的设计原理

利用委托式控制风格，每个界面需要访问的业务逻辑有各自的控制器委托给不同的业务逻辑对象。

## 5、依赖视角

下面两图是前端和后端各自包之间的依赖关系。

1、前端包图

![迭代三前端开发包图](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/%E8%BF%AD%E4%BB%A3%E4%B8%89%E5%89%8D%E7%AB%AF%E5%BC%80%E5%8F%91%E5%8C%85%E5%9B%BE.jpg)

2、后端包图

![迭代三后端开发包图](https://stage3-doc.oss-cn-beijing.aliyuncs.com/HomeworkImgs/%E8%BF%AD%E4%BB%A3%E4%B8%89%E5%90%8E%E7%AB%AF%E5%BC%80%E5%8F%91%E5%8C%85%E5%9B%BE.jpg)

