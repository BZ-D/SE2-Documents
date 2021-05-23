## 4、组合视角

### 4.1、开发包图

"Course-Learning"课程学习网站系统的最终开发设计如下表所示

| 开发（物理）包           | 依赖的其他开发包                                             |
| ------------------------ | ------------------------------------------------------------ |
| mapper                   | ibatis,po                                                    |
| mainui                   | vo, userui, rechargeui, course_orderui, course_wareui, course_manageui, promotionui, fileui |
| userui                   | vueframework,vo,useblservice                                 |
| userbl                   | springframework,useblservice,userdataservice,po              |
| userblservice            | springframework,util                                         |
| userdata                 | databaseutility,po,userdataservice                           |
| userdataservice          | springframework,http rest,po                                 |
| rechargeui               | vueframework,vo,rechargeblservice                            |
| rechargebl               | springframework,rechargeblservice,rechargedataservice,po,userbl |
| rechargeblservice        | springframework,util                                         |
| rechargedata             | databaseutility,po,rechargedataservice                       |
| rechargedataservice      | springframework,http rest,po                                 |
| course_orderui           | vueframework,vo,course_orderblservice                        |
| course_orderbl           | springframework,course_orderblservice,course_orderdataservice,po,userbl,promotionbl |
| course_orderblservice    | springframework,util                                         |
| course_orderdata         | databaseutility,po,course_orderdataservice                   |
| course_orderdataservice  | springframework,http rest,po                                 |
| course_wareui            | vueframework,vo,course_wareblservice                         |
| course_warebl            | springframework,course_wareblservice,course_waredataservice,po,userbl |
| course_wareblservice     | springframework,util                                         |
| course_waredata          | databaseutility,po,course_waredataservice                    |
| course_waredataservice   | springframework,http rest,po                                 |
| course_manageui          | vueframework,vo,course_manageblservice                       |
| course_managebl          | springframework,course_manageblservice,course_managedataservice,po,course_warebl,userbl |
| course_manageblservice   | springframework,util                                         |
| course_managedata        | databaseutility,po,course_managedataservice                  |
| course_managedataservice | springframework,http rest,po                                 |
| promotionui              | vueframework, promotionblservice                             |
| promotionbl              | springframework,promotionblservice,promotiondataservice,po,userbl |
| promotionblservice       | springframework,util                                         |
| promotiondata            | databaseutility,po,promotiondataservice                      |
| promotiondataservice     | springframework,http rest,po                                 |
| vo                       |                                                              |
| po                       | vo                                                           |
| util                     |                                                              |
| http rest                |                                                              |
| vueframework             |                                                              |
| databaseutility          | JDBC                                                         |
| springframework          |                                                              |
| ibatis                   |                                                              |

"Course-Learning"课程学习网站系统的前端开发包图如下图所示：

![课程学习网站系统前端开发包图](https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/课程学习网站系统前端开发包图.jpg)

"Course-Learning"课程学习网站系统的后端开发包图如下图所示：

![课程学习网站系统后端开发包图](https://document3-architecture.oss-cn-beijing.aliyuncs.com/HomeworkImgs/课程学习网站系统后端开发包图.jpg)

