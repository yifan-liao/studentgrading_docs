## 课程(Course)

### 获得课程列表
获得所有课程的列表。

权限: 所有人。但是得到的课程信息因人而异。任课教师，上课学生能查看更多的信息。
```
GET courses/
```

学生获得已选课程列表

**还未实现**。

权限: 学生。
```
GET courses/taking/
```

教师获得任课列表

**还未实现**。

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
### 获得课程学生选课信息列表

权限：任课教师，上课学生

```
GET courses/:id/students/
```

响应：

课程学生获得的列表：

```json
[
  {
    "url": "http://testserver/api/courses/1/students/1/",
    "id": 1,
    "course": "http://testserver/api/courses/1/",
    "student": "http://testserver/api/students/1/",
    "grade": null
  },
  {
    "url": "http://testserver/api/courses/1/students/2/",
    "id": 2,
    "course": "http://testserver/api/courses/1/",
    "student": "http://testserver/api/students/2/"
  }
]
```

任课教师获得的列表：
```json
[
  {
    "url": "http://testserver/api/courses/1/students/1/",
    "id": 1,
    "course": "http://testserver/api/courses/1/",
    "student": "http://testserver/api/students/1/",
    "grade": null
  },
  {
    "url": "http://testserver/api/courses/1/students/2/",
    "id": 2,
    "course": "http://testserver/api/courses/1/",
    "student": "http://testserver/api/students/2/",
    "grade": null
  }
]
```

---
### 获得课程某一学生的选课信息

权限：任课教师，上课学生

```
GET courses/:id/students/
```

学生获得自己的选课信息，或者任课教师：

```json
{
  "url": "http://testserver/api/courses/1/students/1/",
  "id": 1,
  "course": "http://testserver/api/courses/1/",
  "student": "http://testserver/api/students/1/",
  "grade": null
}
```

学生查看其他课程学生：

```json
{
  "url": "http://testserver/api/courses/1/students/2/",
  "id": 2,
  "course": "http://testserver/api/courses/1/",
  "student": "http://testserver/api/students/2/"
}
```

---
### 修改某一课程学生的成绩

权限：任课教师

```json
PATCH courses/:id/students/:id/
```

输入：

| Name | Type | Description
|:---- |:---- |:-------
| grade | decimal string | 课程成绩，0-100之间，最多两位小数

e.g.

```json
{
  "grade": '80.5'
}
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
| student | url | **Required**. 学生。

e.g.

```json
{
  "student": "http://testserver/api/courses/1/"
}
```

---
### 学生退选

权限：任课教师

```json
DELETE courses/:id/students/:id/
```

---
### 添加作业

权限：任课教师

**还未实现**。

```
POST courses/:id/assignments/
```

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

**还未实现**。

权限：任课教师。上课学生。


```
GET courses/:id/students/ungrouped/
```

## 学生(Student)

### 获得学生列表

```
GET students/
```

响应：

学生访问：

```json
[
  {
    "url": "http://testserver/api/students/1/",
    "id": 1,
    "user": "http://testserver/api/users/1/",
    "name": "Joshuah Kertzmann",
    "sex": "M",
    "s_id": "2012211000",
    "s_class": "http://testserver/api/classes/1/",
    "courses": "http://testserver/api/students/1/courses/"
  },
  {
    "url": "http://testserver/api/students/2/",
    "id": 2,
    "name": "Ms. Shira O'Kon",
    "sex": "F",
    "s_id": "2012211001",
    "s_class": "http://testserver/api/classes/1/"
  },
  {
    "url": "http://testserver/api/students/3/",
    "id": 3,
    "name": "Olie Daugherty",
    "sex": "M"
  }
]
```

教师访问：

```json
[
  {
    "url": "http://testserver/api/students/1/",
    "id": 1,
    "name": "Sherilyn Morissette",
    "sex": "M",
    "s_id": "2012211000",
    "s_class": "http://testserver/api/classes/1/",
    "courses": "http://testserver/api/students/1/courses/"
  },
  {
    "url": "http://testserver/api/students/2/",
    "id": 2,
    "name": "Dr. Newton Rutherford II",
    "sex": "F",
    "s_id": "2012211001",
    "s_class": "http://testserver/api/classes/1/",
    "courses": "http://testserver/api/students/2/courses/"
  },
  {
    "url": "http://testserver/api/students/3/",
    "id": 3,
    "name": "Brandee Ziemann",
    "sex": "M",
    "s_id": "2012211002",
    "s_class": "http://testserver/api/classes/2/",
    "courses": "http://testserver/api/students/3/courses/"
  }
]
```

---
### 获得某一学生的信息

```
GET students/:id/
```

响应：

学生获取自己的信息：

```json
{
  "url": "http://testserver/api/students/1/",
  "id": 1,
  "user": "http://testserver/api/users/1/",
  "name": "Joshuah Kertzmann",
  "sex": "M",
  "s_id": "2012211000",
  "s_class": "http://testserver/api/classes/1/",
  "courses": "http://testserver/api/students/1/courses/"
}
```

学生获取同班同学的信息：

```json
{
  "url": "http://testserver/api/students/2/",
  "id": 2,
  "name": "Ms. Shira O'Kon",
  "sex": "F",
  "s_id": "2012211001",
  "s_class": "http://testserver/api/classes/1/"
}
```

学生获取课程同学的信息：

```json
{
  "url": "http://testserver/api/students/3/",
  "id": 3,
  "name": "Olie Daugherty",
  "sex": "M"
}
```

教师获取学生信息：

```json
{
  "url": "http://testserver/api/students/1/",
  "id": 1,
  "name": "Sherilyn Morissette",
  "sex": "M",
  "s_id": "2012211000",
  "s_class": "http://testserver/api/classes/1/",
  "courses": "http://testserver/api/students/1/courses/"
}
```

---
### 获取学生选课信息

```
GET students/:id/courses/
```

响应：
```json
[
  {
    "url": "http://testserver/api/students/1/courses/1/",
    "id": 1,
    "student": "http://testserver/api/students/1/",
    "course": "http://testserver/api/courses/1/",
    "grade": null
  },
  {
    "url": "http://testserver/api/students/1/courses/2/",
    "id": 2,
    "student": "http://testserver/api/students/1/",
    "course": "http://testserver/api/courses/2/",
    "grade": null
  }
]
```

---
### 获取学生某一课程的选课信息

包括成绩信息。

权限：学生自己，任课教师，其他上此课程的学生

```json
GET students/:id/courses/:id/
```

响应：

```json
{
  "url": "http://testserver/api/students/1/courses/1/",
  "id": 1,
  "student": "http://testserver/api/students/1/",
  "course": "http://testserver/api/courses/1/",
  "grade": null
}
```

---
### 修改学生课程成绩

权限：任课教师

```json
PATCH students/:id/courses/:id/
```

输入：

| Name | Type | Description
|:---- |:---- |:-------
| grade | decimal string | 课程成绩，0-100之间，最多两位小数

e.g.

```json
{
  "grade": '80.5'
}
```

---
### 学生选课

权限：任课教师

```json
POST students/:id/courses/
```

输入：

| Name | Type | Description
|:---- |:---- |:-------
| course | url | **Required**. 所选课程

e.g.

```json
{
  "course": "http://testserver/api/courses/1/",
}
```

---
### 学生退选

权限：任课教师

```json
DELETE students/:id/courses/:id/
```


## 小组(Group)

---
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

---
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

---
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

---
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

---
### 删除小组

权限：任课教师。

```
DELETE groups/:id/
```

---
### 添加成员

权限：任课教师，组长。

**还未实现**。

```
POST groups/:id/members/
```

---
### 删除成员

**还未实现**。

权限：任课教师，组长。

```
DELETE groups/:id/members/
```

---
### 获得小组提交的作业列表

**还未实现**。

```
GET groups/:id/submissions/
```
