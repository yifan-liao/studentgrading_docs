## 用户的全局权限

### Student

- `view_student`
- `view_takes`
- `view_course`
- `view_instructor`
- `view_teaches`
- `view_group`, `add_group`, `change_group`

---
### Instructor

- `view_instructor`
- `view_takes`, `change_takes`, `add_takes`, `delete_takes`
- `view_course`, `change_course`, `add_course`, `delete_course`
- `view_student`
- `view_teaches`, `add_teaches`, `delete_teaches`
- `view_group`, `change_group`, `add_group`, `delete_group`

## 资源的权限

### Students(`students/`)

#### Read

- `view_student_base`: url, id, name, sex, (上同一门课的学生)
- `view_student_normal`: url, id, name, sex, s_class,  (同班同学)
- `view_student_advanced`: url, id, name, sex, s_class, s_id, courses (教师)
- `view_student`, (学生自己)

---
### Instructors(`instructors/`)

#### Read
- `view_instructor_base`: name, sex (上课的学生)
- `view_instructor_normal`: name, sex, inst_id (教师)
- `view_instructor` (教师自己)

---
### Course(`courses/`)
#### Read
- `view_course`: url, id, title, year, semester, description, min_group_size, max_group_size, instructors (任课教师, 上课学生)
- `view_course_advanced`: url, id, title, year, semester, description, instructors (其他教师)
- `view_course_normal`: url, id, title, year, semester, description (其他学生)

#### Add
- `add_course`（任课教师）

#### Update
- `change_course_base`: description, min/max goup size (任课教师)
		
#### Delete
- `delete_course` (任课教师)

---
### Takes(`students/{pk}/courses/`, `courses/{pk}/students/`)

#### Read
- `view_takes` (任课教师， 学生自己)
- `view_takes_base` (其他上课学生)

#### Add
- `add_takes` (任课教师)

#### Update
- `change_takes_base`: grade (任课教师)

#### Delete
- `delete_takes` (任课教师）

---
### Teaches(`instructors/{pk}/courses/`)
#### Read
- `view_teaches`（任课教师，上课学生）
		
#### Add
- `add_teaches` (任课教师）

#### Update
- `change_takes`

#### Delete
- `delete_takes` (任课教师）

---
### Groups(`groups/`, `courses/{pk}/groups/`)
#### Read
- `view_group`（任课教师，上课学生）

#### Add
- `add_group` (任课教师, 上课学生）

#### Update
- `change_group_advanced`: name, leader, members (任课教师，组长)

#### Delete
- `delete_group` (任课教师）
