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

#### 响应
```json
[
  {
    "url": "http://testserver/api/courses/1/",
    "id": 1,
    "title": "Poker Theory and Analytics",
    "year": 2015,
    "semester": "SPG",
    "description": "",
    "min_group_size": 0,
    "max_group_size": 0,
    "instructors": "http://testserver/api/courses/1/instructors/"
  },
  {
    "url": "http://testserver/api/courses/2/",
    "id": 2,
    "title": "The Anthropology of Cybercultures",
    "year": 2003,
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

#### 响应

学生查看所选课程，或者教师查看所任课程：
```json
{
  "url": "http://testserver/api/courses/1/",
  "id": 1,
  "title": "Digital Signal Processing",
  "year": 2008,
  "semester": "SPG",
  "description": "",
  "min_group_size": 0,
  "max_group_size": 0,
  "instructors": "http://testserver/api/courses/1/instructors/"
}
```

学生查看未选课程，或者教师查看其他课程：
```json
{
  "url": "http://testserver/api/courses/2/",
  "id": 2,
  "title": "High-Dimensional Statistics",
  "year": 2010,
  "semester": "AUT",
  "description": ""
}
```

---
### 新增课程
```
POST courses/
```

#### 

---
### 设置学生
添加一个学生。
```
POST courses/:id/students/
```

#### 权限
任课教师

---
### 设置作业
```
POST courses/:id/assignments/
```
#### 权限
任课教师

---
### 设置小组
添加一个小组。
```
POST courses/:id/groups/
```
#### 权限
任课教师。上课且没有小组的学生。

---
### 获得没有小组的学生列表
```
GET courses/:id/students/ungrouped/
```
#### 权限
任课教师。上课学生。

---
### 更改课程配置
组员人数限制配置
```
PATCH courses/:id/
```

## 学生(Student)

## 小组(Group)
### 获得小组列表
```
GET groups/
```

### 添加成员
添加一个没有组的上课学生。
```
POST groups/:id/members/
```
#### 权限
任课教师。组长。

### 更换组长
将一个组内成员提升为组长，组长降为组内成员。
```
PUT groups/:id/leader/
```
#### 权限
任课教师。组长。

### 获得作业列表
获得本小组所在课程布置的所有作业：
```
GET groups/:id/assignments/
```
