---
layout: post
title: 왜 우리는 OOP를 사용해야 할까?
date: 2018-09-15
description: 우리가 왜 OOP를 사용하면 좋은지 실제 예시를 사용해 알아보자.
img:  /python/python-logo.png
categories: [Programming, Python]
tags: [Python, OOP]
---

<br>

## 1. 우리는 왜 클래스를 써야하는가

<br>

질문한다. 우리는 왜 클래스를 써야 하냐고. 난 그런거 모른다고.  
그러면 현실의 문제를 해결하면서, 클래스 사용의 당위성을 생각해보면 어떨까?  
이번 내용은 그것에 초점이 맞추어져 있다.  

우선, 난 아무개 고등학교의 '교사'가 되었다고 생각하자.  
교사의 주요 업무 중 하나는 학생들의 성적을 확인하고 관리하는 일인데,  
이 일을 클래스를 쓰지 않고 해보고, 클래스를 써서 리팩토링 해가며 개선해보는 작업을 해보자.  

<br>

## 2. 리팩토링 안 쓰고 해보기


먼저, 이 작업을 클래스를 안 쓰고 리스트 등 기본 자료구조를 써가면서 한다고 해보자.  
내가 할 일은 학생들의 성적을 개개인별로 관리하고, 그것을 반 단위의 학생부로 관리하고 싶은 것이라고 하자.  

일단 내가 관리하는 반에는 5명의 학생이 있고 그들의 정보를 딕셔너리에 담는다고 하자.  
그리고 그들의 정보를 학생부에 추가한다. 추가 순서는 그들의 번호 오름차순이다.  

내 작업폴더에 gradebook.py라는 모듈에 이 정보들을 추가하고 있다.  


```python
gradebook = ['3반'] # 학생들의 정보를 담는 학생부 변수이다. 첫 원소에는 학급의 이름을 담는다고 생각하자.

students_1 = {'name': 'Nayeon', 'Math': 90, 'English': 70, 'Korean': 100}
students_2 = {'name': 'Dahyeon', 'Math': 40, 'English': 65, 'Korean': 70}
students_3 = {'name': 'Momo', 'Math': 89, 'English': 82, 'Korean': 92}
students_4 = {'name': 'Jyeongyeon', 'Math': 50, 'English': 62, 'Korean': 31}
students_5 = {'name': 'Chaeyoung', 'Math': 88, 'English': 20, 'Korean': 60}

gradebook.append(students_1)
gradebook.append(students_2)
gradebook.append(students_3)
gradebook.append(students_4)
gradebook.append(students_5)
```

<br>

일단 여기까지는 무난무난해 보인다.  
현실의 학생 5명을 모델링해서 학생부에 필요 없는 별자리 같은 정보를 지우고 필요한 정보만 남겨 놓았다.   
이 짓을 하는 이유는 당연히 모으는 게 목적이 아닐테고, 슬슬 '관리'에 대한 필요도 생긴다.  

먼저 학생들의 성적을  
1. 학급의 과목별로,  
2. 학생 개개인별로  
구해야 한다고 하자.  

난 프로그래밍을 열심히 배웠기 때문에 이런 작업에는 함수를 쓰는 것이 바람직하다고 알고 있다.  
왜 바람직하지 않은지 잘 모르겠으면 그건 모듈화, 재사용성, 가독성, 전문화, 관리의 용이함 등의 장점을 모르는 것과 같다.  


```python
### 1. 학급의 과목별로 평균 구하기

def grade_average(gradebook, subject):
    name, gradebook = gradebook[0], gradebook[1:]  # packing이 들어갔다.
    n = len(gradebook)  # 학생수 구하기
    average = sum([x[subject] for x in gradebook])  / n # list comprehension이 쓰였지???? 이거 한 줄이면 된다.
    return name + '의 ' + subject + ' 평균은 ' + str(average)
    
print(grade_average(gradebook, 'Math'))
print(grade_average(gradebook, 'Korean'))
print(grade_average(gradebook, 'English'))

>>>    3반의 Math 평균은 71.4
>>>    3반의 Korean 평균은 70.6
>>>    3반의 English 평균은 59.8
```

<br>

```python
### 2. 학생 개개인 별로 성적 구하기
def student_average(gradebook, name):
    for stu in gradebook[1:]:
        if stu['name'] == name:
            student = stu
            break
    math = student['Math']
    korean = student['Korean']
    english = student['English']
    avg = (math + korean + english) / 3
    return avg

student_average(gradebook, 'Nayeon')
```

<br>

여기까지는 그래, 할만 하겠다 싶다.  
지금의 우리의 데이터 구조는 어떻게 되는가?

gradebook은 `list`로, 첫 원소를 학급 이름을, 나머지 원소를 `dict`인 학생들을 담고 있다.  
학생이 dict 특성상 순서가 없다고는 하지만 전체 구조를 2차원이라고 잡을 수 있다.  

우리는 2차원에 익숙하다. 엑셀, 데이터베이스 테이블 등을 2차원 등으로 표현하고 보여주는 것은 다 이유가 있는 것.  

조금 더 나아가서, 반에 'Sana'라는 흐뭇해 지는 학생이 전학 왔다고 하자. 학생부에 정보를 추가해야 한다.


```python
### 3. 학생 추가하기
def add_student(gradebook, name, math, korean, english):
    newbie = {'name': name, 'Math': math, 'Korean': korean, 'English': english}
    gradebook.append(newbie)
    
add_student(gradebook, 'Sana', 50, 60, 70)

gradebook

>>> ['3반',
     {'English': 70, 'Korean': 100, 'Math': 90, 'name': 'Nayeon'},
     {'English': 65, 'Korean': 70, 'Math': 40, 'name': 'Dahyeon'},
     {'English': 82, 'Korean': 92, 'Math': 89, 'name': 'Momo'},
     {'English': 62, 'Korean': 31, 'Math': 50, 'name': 'Jyeongyeon'},
     {'English': 20, 'Korean': 60, 'Math': 88, 'name': 'Chaeyoung'},
     {'English': 70, 'Korean': 60, 'Math': 50, 'name': 'Sana'},
 ]
```

<br>



좋다. 그런데 더 나아가야 한다. 학생들을 관리하는 일은 복잡하다.  
고등학교 학생들은 모의고사를 본다. 그런데 우리 학생부는 최신 정보만 반영하고 있기 때문에  
학생의 발전 모습 등 변화 추이를 관찰할 수 없다.  
따라서 이제는 전국연합학력평가를 치르는 3, 4, 7, 10월 정보를 같이 담는다고 하자.  

또한 학생에 대한 정보를 성적만 담는다는 것은 너무 잔인하다. 취미 등 다양한 정보를 담는다고 하자. 


```python
### 학생 정보 Renewal!

gradebook = ['3반',
 {'English': [45, 75, 67, 70], 'Korean': [100, 97, 97, 100], 'Math': [65, 74, 87, 54], 'name': 'Nayeon',
   'hobbies': ['dance', 'sing'], 'favorite_movies': ['Begin again', 'Chicken run']},
 {'English': [54, 65, 75, 65], 'Korean': [70, 87, 45, 76], 'Math': [40, 54, 65, 65], 'name': 'Dahyeon',
   'hobbies': ['read', 'dringking beer'], 'favorite_movies': ['mugando', 'sinsegye', 'money ball']},
 {'English': [82, 93, 95, 95], 'Korean': [67, 76, 78, 82], 'Math': [67, 87, 65, 87], 'name': 'Momo',
   'hobbies': ['dance', 'Programming'], 'favorite_movies': ['Zootopia', 'Search', '99 homes']},
 {'English': [87, 56, 54, 76], 'Korean': [54, 54, 67, 76], 'Math': [34, 33, 54, 45], 'name': 'Jyeongyeon',
   'hobbies': ['trip'], 'favorite_movies': ['Mother']},
 {'English': [82, 81, 61, 79], 'Korean': [72, 88, 78, 98], 'Math': [67, 78, 33, 45], 'name': 'Chaeyoung',
   'hobbies': ['Movie'], 'favorite_movies': ['Your name...']},
]
```

<br>

아예 student에 대한 구조 자체를 바꿔서 추가했다.  
**정상적인 사람이라면 보기 불편해야 하는데 그 이유는 이제 차원이 3차원으로 넘어 갔기 때문이다.**  
이때, 다양한 정보를 표현하는 함수를 만들텐데 괴로움을 맛보도록 하자.

1. 원하는 시험의 특정 과목의 학생들 평균 알아보기
1. 특정 학생의 특정 분기 특정 과목 성적 알아내기
1. 학생들이 가장 좋아하는 취미가 뭔지 출력하기


```python
# 1. 원하는 시험의 특정 과목의 학생들 평균 알아보기
def students_grades_average(gradebook, which_exam, subject):
    avg = 0
    gradebook = gradebook[1:]
    length = len(gradebook)
    
    for stu in gradebook:
        avg += stu[subject][which_exam]
    return avg / length


# 2. 특정 학생의 특정 분기 특정 성적 알아보기
def get_specific_score(gradebook, name, which, subject):
    for stu in gradebook[1:]:
        if stu['name'] == name:
            student = stu
            break
    
    student[subject][which]
    

# 3. 학생들이 좋아하는 1순위 취미들을 모아 집합으로 반환하기
def what_are_favorite_hobbies(gradebook):
    hobbies = set()
    for stu in gradebook[1:]:
        hobbies = hobbies.union([stu['hobbies'][0]])
    return hobbies
    
    
print(students_grades_average(gradebook, 0, 'Math'))
print(what_are_favorite_hobbies(gradebook))


>>>    54.6
>>>    {'read', 'dance', 'trip'}
```

<Br>

나오기는 나오는데, 불편함을 감추지 않을 수 없다.  
3차원이 되면서 위 2 함수에는 뭔가 불편함이 감돌고 있다.

위에까지를 하나의 모듈로 만들어 학생부 파일로 쓴다고 하자.  
순수하게 파이썬의 기본 데이터 구조만을 사용해 만들었다. 그리고 같은 필요를 느끼는 동료들에게  
잘 쓰라고 파일을 메일로 보내준다. 하지만 많은 경우 이들은 불편함을 느낄 것인데, 그 이유는 다음과 같다.  


1. **모든 함수와 변수가 전역(global) 처리되어 있다.**
  - 이게 크다. **스코프는(namespace라고도 한다.) 정말 꼭 필요한 경우가 아니면 범위를 한정짓는 게 맞다.**   
    예기치 못한 오염의 위험이 있으며, 모든 변수가 한 스코프에 있기 때문에 관리하기도 힘들다.   
    삼성에서 모든 직원을 하나의 부서에 때려 박지 않고, 각종 부서로 나눠 배치하는 것과 같은 이치다.  
    규모가 너무 작은 회사가 아닌 이상, 아무리 수형, 평등을 지향하는 회사라도 부서는 나뉘어져 있다.  
<br>

2. **코드 가독성이 떨어진다.**
  - 자료가 3차원 이상이 되면서 원하는 함수를 만드는데 코드에 매직넘버가 들어가는 등 어려워졌다.
    아까 정의한 새 gradebook만 봐도 가슴이 편치 않음을 느낄 수 있다.
    애초에 **자료구조가 3차원 이상으로 넘어가기 시작하면, 클래스 사용을 진지하게 고려해야 한다.**  

        
3. **전문화가 어렵다.**
  - **모든 변수와 함수가 같은 스코프에 있기 때문에 가령 학생 전문 함수를 만들기가 더 어렵다.**  
    아마 새 함수가 기존의 학생 함수들을 쓸 수도 있는데(의존할 수도 있는데) 함수들이 너무 많아 학생부 변수들도 봐야 한다.  
<br>
    
4. **재사용성이 떨어진다.**
  - 지금은 한 파일에 학생과 관련된 정보, 학생부와 관련된 정보가 혼잡하게 섞여 있어 원하는 정보를 찾기 어렵다.   
    만약 동료 교사가 이것을 사용하려 하면, 원하는 기능 하나를 찾기 위해 이리 저리 함수를 돌아다녀야 한다.<br>  

5. 커스터마이제이션이 어려워진다. 가령 기존의 함수에서 조금씩을 바꿔 쓰고자 한다고 하자.



```python 
### 1. 학급의 과목별로 평균 구하기

def grade_average(gradebook, subject):
    name, *gradebook = gradebook  # packing이 들어갔다.
    n = len(gradebook)  # 학생수 구하기
    average = sum([x[subject] for x in gradebook])  / n # list comprehension이 쓰였지???? 이거 한 줄이면 된다.
    return name + '의 ' + subject + ' 평균은 ' + str(average)
    
print(grade_average(gradebook, 'Math'))
print(grade_average(gradebook, 'Korean'))
print(grade_average(gradebook, 'English'))


>>> 3반의 Math 평균은 71.4
>>> 3반의 Korean 평균은 70.6
>>> 3반의 English 평균은 59.8
```

<br>

  - 아까 만든 함수다. 근데 나는 저렇게 문자열이 아니라 가령 수학 과목의 평균을 숫자로 바꾸고 싶으면,  
조금 바꿔야 한다. 그러면 모듈을 열고 실제 함수를 찾아 코드를 조금 바꿀 것이다.  

  - 이렇게 여러 사람이 만든 코드가 섞이면??? grade_average라는 같은 이름의 함수가 여러 버전으로 존재하게 된다.  
    

<br>
<br>



#### 그러니까, 클래스를 쓰면 이것들을 적어도 완화할 수 있다. 가보자. 

<br>
<br>
<hr>
<br>

## 3. :exclamation: 클래스로 해보기.

난 애초에 만들 때부터 다른 교사들의 사용을 염두해 두고 있다.  
이들은 분명 나와 다른 기능을 원할 수도 있고 해서, 내 생각에 정말 필요한 기능만을 일부 구현해 놓으려고 한다.  

그래서 학생부와 학생 클래스를 만드는데 기본이 되는 BaseGradebook, BaseSudent 클래스를 만들고,  
내가 직접 사용하는 클래스를 그것을 상속해서 쓴다고 하자. 베이스 클래스들은 다음과 같다.


```python
class BaseGradebook:
    def __init__(self, name):
        self.name = name
        self.students = []
        self.length = 0
        
    # gradebook['momo']와 같이 이름을 키로 받았을 때 특정 학생 반환하도록 반환
    def __get__(self, name):
        for stu in self.students:
            if stu.name == name:
                return stu
        
    # 학생 추가하기
    def add_student(self, student):
        self.students.append(student)
        self.length += 1

    # 학급의 특정 시험의 특정 과목 평균 출력
    def average_of_subject_which_exam(self, subject, which_exam):
        tmp_sum = 0
        for stu in self.students:
            tmp_sum += stu[subject][which_exam]
        return tmp_sum / self.length
    

class BaseStudent:
    def __init__(self, name, sex):
        self._math = []
        self._korean = []
        self._english = []
        self._name = name
        self._sex = sex
        self._hobbies = []
        
    def add_exam_result(self, math, korean, english):
        raise NotImplementedError("")

    # 학생의 특정 과목 점수의 평균 반환
    def average_grade_of(self, subject):
        return sum(self[subject])

    def fill_hobbies(self):
        raise NotImplementedError("")

    def print_hobby(self):
        raise NotImplementedError("")
        
test_student = BaseStudent('na', 'f')
test_student['math']


>>> []
```

<br>

기본이 되는 클래스들을 선언했다.  
**이 함수들은 클래스를 만들 때 '이것들은 꼭 필요하겠지?'라는 마인드로 만든 것들이다.**  
많은 경우, 교사들은 이 클래스를 상속해 사용하면 편할 것이다.  

그중에서도 **'이것만큼은 이대로 쓰겠다' 싶은 것들은 직접 완성까지 했고,**  
**교사마다 쓰임이 다를 것이라고 생각한 함수는 NotImplementedError("")를 뱉도록 했다.**  
이는 교사가 받아 쓰면서 만들어 써야 한다.  

이때 `__get__`를 볼 수 있는데 이 메소드는 우리가 `dict`에 `[ ]` 연산으로 키에 맞는 값을 뽑아 내듯이,  
**인스턴스에 [ ] 연산으로 값이 들어왔을 때 어떻게 처리하는지 명령하는 함수다.**  
위와 같이 선언에서 gradebook['Momo']와 같이 사용하면 학생을 바로 뽑아낼 수 있다.  

<br>

이제 나 박성환이 쓸 학생부, 학생 클래스를 만들어 보자.  


```python
class SunghwanGradebook(BaseGradebook):
    """Store gradebook of a class
    
    In functions in this class, you can see 'which_exam' variable a lot of times.
    if which_exam == 0: it's March's exam,
    if which_exam == 1: it's March's exam,
    if which_exam == 2: it's March's exam,
    if which_exam == 3: it's March's exam,
    
    Variables:
        * self.length:  int | number of the students in a class
    
    Functions:
        *  __init__(self, name, teacehr_name):
            :input:
                str | name:  Name of the class
                str | teacher_name: Name of the teacher of the class
            :return:
                instance |  A new instance of a Gradebook
                
        *  get_specific_score(name, subject, which_exam):
            :input:
                str | name: Name of a student wanted.
                str | subject: Name of a subject which belongs to one of math, english, korean
                int | which_exam: exam number
            :return:
                int |  Score of a specific exam of the subject of the student.
    """
    def __init__(self, name, teacher_name):
        super().__init__(name)
        self.teacher_name = teacher_name
        # 기존에 생성자에 교사 이름까지 저장할 수 있도록 확장했다.
    
    # 특정 학생의 특정 학생의 특정 시험 점수를 반환
    def get_specific_score(name, subject, which_exam):
        return self[name][subject][which_exam]
    
    
class Student(BaseStudent):
    # 시험을 볼 때마다 수학, 국어, 영어 점수를 추가
    def add_exam_result(self, math, korean, english):
        self._math.extend(math)
        self._korean.extend(korean)
        self._english.extend(english)

    # student['math'] 처럼 썼을 때 해당 과목 성적을 담은 리스트를 반환
    def __getitem__(self, subject):
        return getattr(self, '_' + subject)
        

    # 새 취미 추가하기
    def fill_hobbies(self, hobby):
        self._hobbies.append(hobby)

    # 학생들의 취미를 한 줄로 출력하기
    def print_hobby(self):
        return ', '.join(self._hobbies)
```

<br>

기존의 베이스에서 내가 필요한 것들만 추가했다. 여기서 눈 여겨볼 점은   

* 먼저 `super()`의 사용.

super는 상속 받은 상위 클래스를 불러오는 함수이다. 난 이 함수의 생성자를 확장하고 싶기 때문에  
먼저 기존 클래스의 생성자를 먼저 실행하고, 그 후에 내가 원하는 기능을 추가했다.  
여기서는 학생부에 교사 이름을 넣고 있다.  

* `__get__`의 사용
**return self[name][subject][which_exam]**. 이 구문을 살펴보자.  

여기서 `self`는 학생부다.
`self[name]`으로 학생을 뽑아내고,  
`self[name][subject]`로 학생의 성적을 담은 리스트를 뽑아냈으며,  
`self[name][subject][which_exam]`로 인덱싱해 특정 시험의 성적을 뽑아낼 수 있었다.


음 어떤가? 실제로 써보자.


```python
gradebook = SunghwanGradebook('3반', '박성환')
stu = Student('모모', 'f')
stu.add_exam_result([1, 1, 1, 1,], [2,2,2,2,], [3,3,3,3,])
gradebook.add_student(stu)

stu = Student('나연', 'f')
stu.add_exam_result([3,3,3,3,], [4,3,4,2], [2,1,5,4])
gradebook.add_student(stu)

stu = Student('정연', 'f')
stu.add_exam_result([7,6,4,2], [9,7,2,9], [7,5,2,7])
gradebook.add_student(stu)


gradebook.average_of_subject_which_exam('math', 2)



>>> 2.6666666666666665
```

<br>
아까 클래스 밑에 이상한 문자열을 쑤셔 박은 것을 기억하는가?  
그것의 사용처는 다음과 같다.
<br>

```python
help(SunghwanGradebook)

    Help on class SunghwanGradebook in module __main__:
    
    class SunghwanGradebook(BaseGradebook)
     |  Store gradebook of a class
     |  
     |  In functions in this class, you can see 'which_exam' variable a lot of times.
     |  if which_exam == 0: it's March's exam,
     |  if which_exam == 1: it's March's exam,
     |  if which_exam == 2: it's March's exam,
     |  if which_exam == 3: it's March's exam,
     |  
     |  Variables:
     |      * self.length:  int | number of the students in a class
     |  
     |  Functions:
     |      *  __init__(self, name, teacehr_name):
     |          :input:
     |              str | name:  Name of the class
     |              str | teacher_name: Name of the teacher of the class
     |          :return:
     |              instance |  A new instance of a Gradebook
     |              
     |      *  get_specific_score(name, subject, which_exam):
     |          :input:
     |              str | name: Name of a student wanted.
     |              str | subject: Name of a subject which belongs to one of math, english, korean
     |              int | which_exam: exam number
     |          :return:
     |              int |  Score of a specific exam of the subject of the student.
     |  
     |  Method resolution order:
     |      SunghwanGradebook
     |      BaseGradebook
     |      builtins.object
     |  
     |  Methods defined here:
     |  
     |  __init__(self, name, teacher_name)
     |      Initialize self.  See help(type(self)) for accurate signature.
     |  
     |  get_specific_score(name, subject, which_exam)
     |  
     |  ----------------------------------------------------------------------
     |  Methods inherited from BaseGradebook:
     |  
     |  __get__(self, name)
     |  
     |  add_student(self, student)
     |  
     |  average_of_subject_which_exam(self, subject, which_exam)
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors inherited from BaseGradebook:
     |  
     |  __dict__
     |      dictionary for instance variables (if defined)
     |  
     |  __weakref__
     |      list of weak references to the object (if defined)
```    

<br>

어떤가? 이런 구분은 적어도 맨 처음에 무식한 방법보다 몇 가지는 낫다.


1. **특정 학생부와 학생이 자신 고유의 범위 안에 있다. 따라서 오염 등의 문제가 없다.**  
  - 아까와 비교해보자. 아까는 `add_student(gradebook, name, math, korean, english):`처럼  **함수가 학생부를 받았다.**
    하지만 이번에는 `gradebook.add_student(student)`처럼 **학생부가 자신의 함수를 호출해 쓴다.
    오염의 문제가 없을 뿐만 아니라, 함수 실행 시 잘못 된 입력을 넣을 가능성도 줄어든다.

2. **전문화가 보다 쉽다.**
  - 코드가 학생과 학생부로 나뉘어 좀더 그 클래스에 특화된 함수를 만들 수 있다.
    그러니까 코드의 책임영역이 나뉘었다.
    
3. **재사용성이 좋다.(가독성이 좋다.)**
  - 사용할 때 더 쉽지 않은가? 가독성도 더 좋다고 말해달라.
    
4. **customization이 매우 쉬워졌다.**
  - Base 클래스를 만들어 좀더 초반부터 닦고 싶은 사람은 이 클래스를 상속 받아 기능을 구현할 수 있고,  
    누구는 SunghwanGradebook를 그대로 가져다 쓸 수도 있으며,  
    또 SunghwanGradebook를 상속해서 쓸 수도 있을 것이다. 이렇게 되면  
    이름이 충돌해 문제가 생길리 없다.
5. **문서화가 더 쉬워졌다.**
  - 언제 어디서나 문서화는 좋은 관리 방안이다.  
    클래스 선언 바로 밑에 파이썬에서 `docstring`이라고 부르는 문자열을 추가했다.  
    그러면 **`help(SunghwanGradebook)`과 같이 쓰면 그 문자열이 출력되어**  
    **사용시 유용한 문자열을 확인할 수 있다.**
  - 그러니까 클래스에는 다루는 클래스에 대한 무수한 정보가 있지만,  
    **클래스를 감싸고 자신의 메소드라는 인터페이스만 남기고,**  
    **이를 문서화해 사용하는 사람은 클래스에 대한 무수하고 잡스러운 정보를 기억할 필요 없이**  
    클래스를 사용할 수 있게 되었다.

<br>
<br>

<hr>
<br>

# 4. 마치며

<br>

이 예시는 어떤 경우에는 OOP를 쓰는 것이 더 낫다는 것을 설득하기 위해 만들었다.  
함수를 짜다 만 것도 있고, 꼭 필요한 함수를 적지 않기도 했다.  
하지만 요지는 파악 되었을 것이라 생각한다.  

기억하자.

**쓰는 데이터구조가 3차원 이상으로 넘어가게 되면,**  
**우리가 익숙한 인지 구조를 넘어서기 때문에 클래스를 사용해 인터페이스를 편하게 하는 것이 낫다.**
