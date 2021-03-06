# 用户信息相关API

> 所有API中需要用到的`operationID`为随机字符串，通常用于定位问题使用，建议每一次API调用均采用唯一ID，可通过npm包uuid生成。<br/>存在callback的API，callback的回调参数格式为统一格式，errCode为0则代表操作成功，否则为失败。具体参考[此处说明]()。

| 方法            | 描述                   |
| --------------- | ---------------------- |
| getUsersInfo    | 根据userID获取用户资料 |
| getSelfUserInfo | 获取当前登录用户资料   |
| setSelfInfo     | 修改当前登录用户资料   |
| uploadFile      | 上传文件               |



## getUsersInfo

> 根据用户ID获取用户资料，可批量获取。

- Example:

  ```js
  openIM.getUsersInfo(operationID,userIDList,({data}) => {
  	...
  })
  ```

- Parameters:

  | Name       | Type     | Required | Description |
  | ---------- | -------- | -------- | ----------- |
  | userIDList | string[] | true     | 用户ID数组  |


- CallBack:

  | Name | Type   | Description                    |
  | ---- | ------ | ------------------------------ |
  | data | string | [用户信息对象]()列表Json字符串 |


## getSelfUserInfo

> 获取当前登录用户资料。

- Example:

  ```typescript
  openIM.getSelfUserInfo(operationID,({data}) => {
  	...
  })
  ```
  
- CallBack:

  | Name | Type   | Description                            |
  | ---- | ------ | -------------------------------------- |
  | data | string | 当前登录[用户个人信息对象]()Json字符串 |



## setSelfInfo

> 修改当前用户资料。

- Example:

  ```typescript
  const userInfo = {
    userID:"1234",
    nickname: "blooming",//用户昵称
    faceURL: "xxx.com",//头像URL
    gender:1,//性别，0未知，1男，2女
    phoneNumber:"123",//用户手机号
    birth:1642584426,//用户生日
    email:"123@qq.com",//用户邮箱
    ex:"ex"//用户扩展信息
  }
  openIM.setSelfInfo(operationID,userInfo,({data}) => {
  	...
  })
  ```
  
- Parameters:

  | Name        | Type   | Required | Description           |
  | ----------- | ------ | -------- | --------------------- |
  | userID      | string | true     | 用户ID                |
  | nickname    | string | false    | 用户昵称              |
  | faceURL     | string | false    | 用户头像              |
  | gender      | number | false    | 性别：0未知，1男，2女 |
  | phoneNumber | string | false    | 手机号                |
  | birth       | number | false    | 出生日期（时间戳）    |
  | email       | string | false    | 邮箱地址              |
  | ex          | string | false    | 扩展字段              |

- CallBack:

  | Name | Type   | Description          |
  | ---- | ------ | -------------------- |
  | data | string | 用户资料是否修改成功 |



## uploadFile

> 通过SDK上传文件

- Example:

  ```js
  openIM.uploadFile(operationID,filePath)
  ```

- Parameters:

  | Name     | Type   | Required | Description  |
  | -------- | ------ | -------- | ------------ |
  | filePath | string | true     | 文件绝对路径 |


- CallBack:

  > 上传回调通过监听返回，回调与文件可根据上传时的operationID进行一一对应。

  | 事件               | 描述         | 响应                                                     |
  | ------------------ | ------------ | -------------------------------------------------------- |
  | uploadFileFailed   | 文件上传失败 | errCode:错误码<br/>errMsg:错误信息<br>operationID:操作ID |
  | uploadFileProgress | 文件上传进度 | progress:上传进度<br>operationID:操作ID                  |
  | uploadFileSuccess  | 文件上传成功 | data:上传结果<br/>operationID:操作ID                     |


## 

# 用户相关回调

> 相关回调需要通过导入`globalEvent`进行监听，引入步骤参考[SDK引入]()。

| 事件              | 描述                     | 响应                       |
| ----------------- | ------------------------ | -------------------------- |
| onSelfInfoUpdated | 当前登录用户个人信息改变 | 用户个人信息对象json字符串 |
