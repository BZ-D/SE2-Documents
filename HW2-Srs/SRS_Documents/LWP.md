# 需求规格说明模板
### 3.2 功能需求
#### 3.2.7  生成课程订单
##### 3.2.7.1 特征描述

在登录的状态下，学生用户点击“购买课程”按键后，系统依次提示学生用户再次确认是否购买、检索历史订单是否已购买该课程、检查账户余额是否满足购买以及提示是否购买成功。

优先级 = 中

##### 3.2.7.2 刺激/响应序列

- 刺激：学生用户点击“购买课程” 按键
- 响应：系统显示“是否花费【X元】购买课程【XXXXXX】”
- 刺激：学生用户点击“确认”按键
- 响应：系统检索历史订单和账户余额后显示“购买成功”
- 刺激：学生用户点击网页右上角的 **···** 标识
- 响应：系统在 **···** 标识下方弹出单选框，包含”历史订单“、”个人中心“、”登出“选项
- 刺激：学生用户在 **···** 标识下方弹出的单选框中单击”历史订单“选项
- 响应：系统跳转到”历史订单“页面，并在该页面显示此用户已购买的课程订单（包括课程名称）、未支付的课程订单（包括课程名称）、订单创建时间、订单支付时间。对于已购买的课程，订单下方额外添加一个”学习课程“按钮；对于未支付的课程，订单下方额外添加一个”去支付“按钮

##### 3.2.7.3 相关功能需求

| 执行对象                      | 对象描述                                                     |
| ----------------------------- | ------------------------------------------------------------ |
| StudentLayout                 | 系统应该为学生用户展示一个主页页面，页面上有各种课程的信息可供用户浏览 |
| StudentLayout.Buy             | 在学生点击“购买课程”按键时，系统要提示学生确认够买该课程     |
| CourseOrder.verify            | 学生用户点击“确认”按键后，系统通过检查该学生用户的账户余额和历史订单列表来核实能否可以购买该课程 |
| StudentLayout.Confirm         | 学生用户点击“确认”按键，系统显示”购买成功“的信息             |
| StudentLayout.Confirm.Invalid | 学生用户点击“确认”按键，由于学生用户账户余额不足，系统保存未支付订单信息，并提示“当前账户余额不足，购买失败” |
| CourseOrder.Buy               | 学生用户点击“确认”按键，在系统显示“购买成功”后在数据库中添加一条该订单信息 |
| StudentLayout.Check           | 学生用户点击”查看订单“按键，系统要跳转到历史订单的页面显示订单信息，参见Student.HistoryOrder |
| Student.HistoryOrder          | 系统应该为学生用户展示一个历史订单页面，包括已购买的课程订单（包括课程名称）、未支付的课程订单（包括课程名称）、订单创建时间、订单支付时间。对于已购买的课程，订单下方额外添加一个”学习课程“按钮；对于未支付的课程，订单下方额外添加一个”去支付“按钮 |



#### 3.2.10  支付课程订单

##### 3.2.7.1 特征描述

在登陆的状态下，学生用户点击课程订单中的“支付课程”按键，系统依次提示学生用户再次确认支付课程、检索账户余额、完成支付流程。

优先级 = 高

##### 3.2.7.2 刺激/响应序列

- 刺激：学生用户点击网页右上角的 **···** 标识
- 响应：系统在 **···** 标识下方弹出单选框，包含”历史订单“、”个人中心“、”登出“选项
- 刺激：学生用户在 **···** 标识下方弹出的单选框中单击”历史订单“选项
- 响应：系统跳转到”历史订单“页面，并在该页面显示此用户已购买的课程订单（包括课程名称）、未支付的课程订单（包括课程名称）、订单创建时间、订单支付时间。对于已购买的课程，订单下方额外添加一个”学习课程“按钮；对于未支付的课程，订单下方额外添加一个”去支付“按钮
- 刺激：学生用户点击所要支付课程的“支付课程”按键
- 响应：系统提示用户是否利用余额购买课程
- 刺激：学生用户点击“确认”按键
- 响应：系统显示课程购买成功的信息

##### 3.2.1.3 相关功能需求

| 执行对象              | 对象描述                                                     |
| --------------------- | ------------------------------------------------------------ |
| StudentLayout         | 系统应该为学生用户展示一个主页页面，页面上有各种课程的信息可供用户浏览 |
| StudentLayout.check   | 学生用户点击”查看订单“按键，系统要跳转到历史订单的页面显示订单信息，参见Student.HistoryOrder |
| StudentLayout.Pay     | 学生用户点击“支付课程”按键，系统要提示学生用户是否利用余额购买课程 |
| CourseOrder.verify            | 学生用户点击“确认”按键后，系统通过检查该学生用户的账户余额和历史订单列表来核实能否可以购买该课程 |
| StudentLayout.Confirm | 学生用户点击“确认”按键，系统显示”购买成功“的信息             |
| CourseOrder.Buy               | 学生用户点击“确认”按键，在系统显示“购买成功”后在数据库中添加一条该订单信息 |

