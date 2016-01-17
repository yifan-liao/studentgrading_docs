## 课程(Course)

### 获得课程列表
获得所有课程的列表。

权限: 所有人。但是得到的课程信息因人而异。任课教师，上课学生能查看更多的信息。
```
GET courses/
```

学生获得已选课程列表

权限: 学生。
```
GET courses/taking/
```

教师获得任课列表

权限: 教师。
```
GET courses/giving/
```

响应：
```json
[
  {
    "url": "http://testserver/api/courses/1/",
    "id": 1,
    "title": "Urbanizing China: A Reflective Dialogue",
    "year": 2009,
    "semester": "SPG",
    "description": "",
    "min_group_size": 0,
    "max_group_size": 5,
    "instructors": [
      "http://testserver/api/courses/1/instructors/1/",
      "http://testserver/api/courses/1/instructors/2/"
    ],
    "groups": [
      "http://testserver/api/groups/1/",
      "http://testserver/api/groups/2/"
    ]
  },
  {
    "url": "http://testserver/api/courses/2/",
    "id": 2,
    "title": "Poker Theory and Analytics",
    "year": 2013,
    "semester": "AUT",
    "description": ""
  }
]
```

---
### 获得某一课程信息
```
GET courses/:id/
```

响应：

上课学生查看，或者任课教师查看：
```json
{
  "url": "http://testserver/api/courses/1/",
  "id": 1,
  "title": "Urbanizing China: A Reflective Dialogue",
  "year": 2009,
  "semester": "SPG",
  "description": "",
  "min_group_size": 0,
  "max_group_size": 5,
  "instructors": [
    "http://testserver/api/courses/1/instructors/1/",
    "http://testserver/api/courses/1/instructors/2/"
  ],
  "groups": [
    "http://testserver/api/groups/1/",
    "http://testserver/api/groups/2/"
  ]
}
```

未选课学生查看，或者非任课教师查看：
```json
{
  "url": "http://testserver/api/courses/2/",
  "id": 2,
  "title": "Poker Theory and Analytics",
  "year": 2013,
  "semester": "AUT",
  "description": ""
}
```

---
### 新增课程
权限：教师
```
POST courses/
```

输入:

| Name | Type | Description
|:---- |:---- |:-------
| title | string | **Required**. 课程名。
| year | string | **Required**. 课程年份。
| semester | string | **Required**. 取值为`"SPG"`或者`"AUT"`二选一。
| description | string | 课程描述。默认为`''`。
| min_group_size | integer | 课程小组人数最小值。默认为`0`。
| max_group_size | integer | 课程小组人数最大值。默认为`5`。
| instructors | list of urls | 课程教师。默认为`[]`。

e.g.
```json
{
  "description": "Given by dxiao.",
  "instructors": [
    "http://testserver/api/instructors/1/"
  ],
  "semester": "AUT",
  "yaer": "2015",
  "title": "Software Engineering"
}
```

---
### 编辑课程

权限：任课教师

```
PATCH /courses/:id/
```

输入：

| Name | Type | Description
|:---- |:---- |:-------
| description | string | 课程描述
| max_group_size | integer | 小组人数最大值
| min_group_size | integer | 小组人数最小值

小组人数最小值必须小于或等于最大值。

e.g.
```json
{
  "description": "foobar",
  "max_group_size": 4,
  "min_group_size": 1
}
```

---
### 删除课程

权限：任课教师

```
DELETE courses/:id/
```

---
### 添加学生

权限: 任课教师
```
POST courses/:id/students/
```
输入：

| Name | Type | Description
|:---- |:---- |:-------
| student | url | **Required**. 

e.g.
```json
{
  "student": "http://testserver/api/courses/1/"
}
```

---
### 添加作业
```
POST courses/:id/assignments/
```
#### 权限
任课教师

___
### 查看课程小组列表

权限：课程教师，上课学生。

```
GET courses/:id/groups/
```

响应：

```json
[
  {
    "url": "http://testserver/api/groups/1/",
    "id": 1,
    "number": "A",
    "name": "maiores",
    "course": "http://testserver/api/courses/1/",
    "leader": "http://testserver/api/students/1/",
    "members": [
      "http://testserver/api/groups/4/",
      "http://testserver/api/groups/6/"
    ]
  },
  {
    "url": "http://testserver/api/groups/2/",
    "id": 2,
    "number": "B",
    "name": "iste",
    "course": "http://testserver/api/courses/1/",
    "leader": "http://testserver/api/students/2/",
    "members": [
      "http://testserver/api/groups/5/",
      "http://testserver/api/groups/7/"
    ]
  }
]
```

---
### 查看某一课程小组


权限：课程教师，上课学生。

```
GET courses/:id/groups/:id/
```

响应：
```json
{
  "url": "http://testserver/api/groups/1/",
  "id": 1,
  "number": "A",
  "name": "maiores",
  "course": "http://testserver/api/courses/1/",
  "leader": "http://testserver/api/students/1/",
  "members": [
    "http://testserver/api/groups/4/",
    "http://testserver/api/groups/6/"
  ]
}
```


---
### 添加小组

权限：任课教师，上课且没有小组的学生。
```
POST courses/:id/add_group/
```
输入：

| Name | Type | Description
|:---- |:---- |:-------
| name | string | **Required**. 小组名称
| leader | url | **Required**. 组长
| members | list of urls | 组员

备注：组员组长必须为上此课且没有小组的学生。

e.g.
```json
{
  "members": [
    "/api/students/2/",
    "/api/students/3/"
  ],
  "name": "success",
  "leader": "/api/students/1/"
}
```

---
### 获得没有小组的学生列表
```
GET courses/:id/students/ungrouped/
```
#### 权限
任课教师。上课学生。


## 学生(Student)

## 小组(Group)
### 获得小组列表
```
GET groups/
```

响应：

```json
[
  {
    "url": "http://testserver/api/groups/1/",
    "id": 1,
    "number": "A",
    "name": "itaque",
    "course": "http://testserver/api/courses/1/",
    "leader": "http://testserver/api/students/1/",
    "members": [
      "http://testserver/api/groups/4/",
      "http://testserver/api/groups/6/"
    ]
  },
  {
    "url": "http://testserver/api/groups/2/",
    "id": 2,
    "number": "B",
    "name": "sit",
    "course": "http://testserver/api/courses/1/",
    "leader": "http://testserver/api/students/2/",
    "members": [
      "http://testserver/api/groups/5/",
      "http://testserver/api/groups/7/"
    ]
  }
]
```

### 获得某一小组的信息
```
GET groups/:id/
```

响应：
```json
{
  "url": "http://testserver/api/groups/1/",
  "id": 1,
  "number": "A",
  "name": "itaque",
  "course": "http://testserver/api/courses/1/",
  "leader": "http://testserver/api/students/1/",
  "members": [
    "http://testserver/api/groups/4/",
    "http://testserver/api/groups/6/"
  ]
}
```

### 修改小组信息
修改小组名称。

权限：任课教师，组长。
```
PATCH groups/:id/
```

输入：

| Name | Type | Description
|:---- |:---- |:-------
| name | string | 组名

e.g.
```json
{
  "name": "success",
}
```

### 更换组长
将一个组内成员提升为组长，组长降为组内成员。

权限：任课教师，组长。
```
PATCH groups/:id/
```

输入：
| Name | Type | Description
|:---- |:---- |:-------
| leader | url | 组长

e.g.
```json
{
  "leader": "http://testserver/api/students/1/",
}
```

### 删除小组

权限：任课教师。

```
DELETE groups/:id/
```


### 添加成员

权限：任课教师，组长。
```
POST groups/:id/members/
```

### 删除成员
权限：任课教师，组长。
```
DELETE groups/:id/members/
```

### 获得小组提交的作业列表
```
GET groups/:id/submissions/
```
