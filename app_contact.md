# 通讯录接口

请求接口地址:  `http://domain_name:88/danaapi/api/contact/index`
**注： 请自行替换domain_name为可用的域名.**
**说明： **

1,  只能对个人通讯录进行共享， 客户通讯录只能在共享客户的时候才能查看客户的联系人信息.
2,  共享后的信息只能查看不能编辑或者删除，对于记录只有记录的所有者才能进行编辑和删除操作.
3,  标注为`TODO`的接口暂时没有实现.


**<font color="red">标注为TODO的接口是暂时没有实现的接口.</font>**

支持的接口命令:

命令|描述
---|---
Add| 添加通讯录. ( OK )
List| 获得符合条件的通讯录  (OK)
Edit| 编辑通讯录  ( OK )
Del| 删除通讯录.  ( OK )
ShareSet|共享设置. ( OK )
ShareList| 获取我共享给别人的。 ( OK )
ShareMe| 获取别人共享给我的.  ( OK )
MsgList| 获取符合条件的MSG ( TODO )
MsgAdd| 添加新的MSG,参见 core_msg 文档. ( TODO ) 

## 添加通讯录 (Add)
**<font color=green>请求样例：</font> **

    {"token":"400e2e5a-b971-428b-a78f-c669382dc887"
    ,"cmd":"Add"
    ,"body":{
        "name":"姓名"
        ,"work_title": "职称"
        ,"address": "住址"
        ,"company": "公司名称"
        ,"types": 1
        ,"mark": "备注"
        ,"items":[{"type": 1, "value": "值", "is_default": 0}]
    }
    ,"page":0
    ,"page_size":0}

**<font color=red>参数说明:</font> **

字段名称|类型|描述
---|---|---
`token`|string| sessionKey
`cmd`|string| Add
`body`|string|参见后续描述
`page`|int| 0
`page_size`|int|0

**<font color=red>Body参数说明:</font> **

字段名称|类型|描述
---|---|---
`name`|string| 联系人姓名.
`work_title`|string| 联系人职称.
`address`|string| 住址.
`company`|string| 公司名称.
`types`|int| 1, 个人通讯录; 2, 客户通讯录
`mark`|string| 备注.
`items`|array| 用户联系人记录的项目，参见后续说明.

**<font color=red>items参数说明:</font> **

字段名称|类型|描述
---|---|---
`type`|int| 1,住宅电话; 2,单位电话;3,住宅传真;4,单位传真;5,手机号码;6,QQ号码;7,邮件地址;8,skype地址;9,微信号.
`value`|string|type对应的值.
`is_default`|int|0,不是默认记录;1,是默认记录


---

**<font color=green>返回样例：</font> **

    {"code":0
    ,"core_msg":""
    ,"body":[{"unique_id": 1}]
    , "count":0}
    
**<font color=red>Body参数说明:</font> **

字段名称|类型|描述
---|---|---
unique_id|int|返回系统标示该用户的唯一ID,即是系统的id.


## 获得符合条件的通讯录 (List)

**<font color=green>请求样例：</font> **

    {"token":"400e2e5a-b971-428b-a78f-c669382dc887"
    ,"cmd":"List"
    ,"body":{"unique_id": 1, "name": 用户名, "types": 1 }
    ,"page":1
    ,"page_size": 10}

**<font color=red>参数说明:</font> **

字段名称|类型|描述
---|---|---
`token`|string| sessionKey.
`cmd`|string| List
`body`|string| 参见后续说明
`page`|int| 必须大于0
`page_size`|int| 必须大于0

**<font color=red>Body参数说明:</font> **

字段名称|类型|描述
---|---|---
`unique_id`|int| 需要获得一个唯一ID的通讯录信息,如果忽略该值则为0.
`name`|string| 检索用户名,如果忽略该值则为空:"".
`types`|int| 1, 个人通讯录; 2, 客户通讯录；如果要获得所有则为0.


---

**<font color=green>返回样例：</font> **

    {"code":0,"core_msg":""
    ,"body":[
        {
            "unique_id": 1
            ，"name":"姓名"
            ,"work_title": "职称"
            ,"address": "住址"
            ,"company": "公司名称"
            ,"types": 1
            ,"mark": "备注"
            ,"items":[{"type": 1, "value": "值", "is_default": 0}]
        }
        
    ]
    , "count":100}
    
**<font color=red>Body参数说明:</font> **

参见Add接口请求字段的参数说明.


## 编辑通讯录 (Edit)

**<font color=green>请求样例：</font> **

    {"token":"400e2e5a-b971-428b-a78f-c669382dc887"
    ,"cmd":"Edit"
    ,"body":{
        "unique_id": 1
        ,"name":"姓名"
        ,"work_title": "职称"
        ,"address": "住址"
        ,"company": "公司名称"
        ,"types": 1
        ,"mark": "备注"
        ,"items":[{"type": 1, "value": "值", "is_default": 0}]
    }
    ,"page":0
    ,"page_size":0}

**<font color=red>Body参数说明:</font> **

参见Add接口请求字段的参数说明.

---

**<font color=green>返回样例：</font> **

    {"code":0
    ,"core_msg":""
    ,"body":""
    , "count":0}
    


## 删除通讯录 (Del)

可以同时删除多条记录.

**<font color=green>请求样例：</font> **

    {"token":"400e2e5a-b971-428b-a78f-c669382dc887"
    ,"cmd":"Del"
    ,"body":[{
        "unique_id": 1
    }]
    ,"page":0
    ,"page_size":0}

**<font color=red>Body参数说明:</font> **


字段名称|类型|描述
---|---|---
unique_id|int| 删除的唯一标识ID.

---

**<font color=green>返回样例：</font> **

    {"code":0
    ,"core_msg":""
    ,"body":""
    , "count":0}
    
## 共享设置 (ShareSet)

**<font color=green>请求样例：</font> **

    {"token":"400e2e5a-b971-428b-a78f-c669382dc887"
    ,"cmd":"ShareSet"
    ,"body":[{
        "unique_id": 1
        ,"share_uid": 1
        ,"share_flag": 1
    }]
    ,"page":0
    ,"page_size":0}

**<font color=red>Body参数说明:</font> **


字段名称|类型|描述
---|---|---
unique_id|int| 唯一标识ID.
share_uid|int| 员工通讯录中的标识ID.
share_flag|int| 1 设置共享；0 取消共享

---

**<font color=green>返回样例：</font> **

    {"code":0
    ,"core_msg":""
    ,"body":""
    ,"count":0}
    
    
## 获取我共享给别人的通讯录 (ShareList)

**<font color=green>请求样例：</font> **

    {"token":"400e2e5a-b971-428b-a78f-c669382dc887"
    ,"cmd":"ShareList"
    ,"body":[{"unique_id": 1}]
    ,"page":1
    ,"page_size": 10}

**<font color=red>Body参数说明:</font> **

字段名称|类型|描述
---|---|---
`unique_id`|int| 需要获得一个唯一ID的通讯录信息,该值必须大于0.


---

**<font color=green>返回样例：</font> **

    {"code":0
    ,"core_msg":""
    ,"body":[{"unique_id": 1, "share_uid": 2}]
    ,"count":0}
    

**<font color=red>Body参数说明:</font> **

字段名称|类型|描述
---|---|---
`unique_id`|int| 需要获得一个唯一ID的通讯录信息,该值必须大于0.
`share_uid`|int| 被共享者ID.

## 获取别人共享给我的通讯录 (ShareMe)

**<font color=green>请求样例：</font> **

    {"token":"400e2e5a-b971-428b-a78f-c669382dc887"
    ,"cmd":"ShareMe"
    ,"body":""
    ,"page":1
    ,"page_size":10}

**<font color=red>Body参数说明:</font> **

无

---

**<font color=green>返回样例：</font> **

    {"code":0,"core_msg":""
    ,"body":[
        {
            "owner_uid": 1
            ,"unique_id": 1
            ，"name":"姓名"
            ,"work_title": "职称"
            ,"address": "住址"
            ,"company": "公司名称"
            ,"types": 1
            ,"mark": "备注"
            ,"items":[{"type": 1, "value": "值", "is_default": 0}]
        }
        
    ]
    , "count":100}
    
**<font color=red>Body参数说明:</font> **

字段名称|类型|描述
---|---|---
`owner_uid`|int| 这条记录所属ID.

**其余字段参见Add接口请求字段的参数说明.**






