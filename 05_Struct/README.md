# 12. 구조체 (Stucture)

## 변수 묶음
* 하나의 점수를 저장 하기 위해서 변수를 사용 하였다. 

```
int score = 90;
```

* 여러 과목의 점수를 저장 하기 위해서 배열을 사용 하였다.

```
int names[] = {90, 85, 95, 90};
```

* 여러 과목의 점수를 저장 하는데, 각 과목 점수에 대한 정보(과목이름, 석차)를 같이 저장 할 수는 없을까??
* 같은 형태의 여러 정보를 변수로 만들고 하나로 묶어서 하나의 변수로 관리 할 수는 없을까?  

>  ex)  
> 성적 (과목이름, 점수, 석차)  
> 사람(이름, 전화번호, 성별, 생년월일)  
> 핸드폰(제조사, 모델명, 전화 번호) 

## struct
* 여러 변수를 묶어서 하나로 관리 하기 위한 설계도
* 어떤 정보를 어떤 변수에 넣어 사용 할지를 정의 한다. 
* 새로운 type을 만든다고 생각 하면 된다. 

```
struct ScoreData {
    int score;
    char name[32];
};
```
* 위 와 같은 형태로 만들어 준다. 
* 이렇게 같은 목적의 자료를 하나로 묶어서 사용하는 것을 **구조체(structure)** 라고한다
* 이렇게 새로운 struct 를 설계하여 만드는 것을 **정의** 한다고 한다. 
* 함수를 만들 듯이 main 함수 밖에서 선언해 주어야 한다. 
* 함수 처럼 만드는 것은 설계도 일뿐 선언을 하고 사용을 해야 의미가 있다. 

`struct ScoreData `   

* struct 키워드 뒤에 사용할 이름을 정하고 적어 준다.
* 이름은 대문자로 시작하게 만들어 준다. 

```
int score;
char name[32];
```
* 묶어서 관리할 변수를 정해 준다. 
* 최대한 연관성을 지닌 변수만 묶어 주는 것이 좋다. 
* 변수와 다르게 여러 타입을 나타 낼 수 있다. 
* 이렇게 struct 를 구성하는 변수를 **멤버 변수** 라고 부른다.

## struct 선언
```
struct ScoreData scoreData1 = {.score = 100, .name = "국어"};
```

* 설계한 새로운 struct 를 사용 하는 방법이다. 
* struct 키워드 뒤에 새로 만든 이름을 써주고 그 뒤에 변수 이름을 써준다. 
* 값을 넣을때는 . 뒤에 struct 내의 변수 이름을 써주고 값을 넣어 준다. 

```
struct ScoreData scoreData2 = {100, "국어"};
```

* 위와 같은 형태로 순서대로 나열해서 값을 넣을 수도 있다. 

## struct 접근

```
printf("%s의 점수는 %d점 이다.\n", scoreData1.name, scoreData1.score);
scoreData1.score = 80;
```
* 값을 접근 할때는 struct 변수명 뒤에 **.** 을 붙이고, 멤버변수를 적어 주면 된다. 
* 값을 접근하고 변경 하는 방법은 기존 변수와 동일 하다. 

```
sprintf(scoreData1.name, "%s", "수학");
strcpy(scoreData1.name, "수학");
```
* 단, 문자열의 경우 선언하고 초기화에서는 바로 문자열을 넣어 줄수 있지만, 선언 이후에 값을 변경할때는 sprintf, 나 strcpy 등을 통해서 값을 변경해 주어야 한다. 


## typedef

* int, double, char 등을 타입을 재정의 하여 사용 할 수 있다.

```
typedef char alphabet;
typedef unsigned int price;
```
* typedef 키워드 뒤에 기존에 있는 타입을 적어 주고, 그 뒤에 새롭게 만들 이름을 정해 준다. 
* 일반적으로 특정한 목적을 위해서 구분을 위해 새로운 별명을 짓는 용도로 사용된다. 
* 가끔 긴 타입을 줄이기 위해서도 사용 될 수 있다. 

```
alphabet abc = 'A';
price money = 1300;
```

* 위처럼 변수를 선언할때 새로운 타입을 변수 타입처럼 사용 하면 된다. 

## typedef struct 

* typedef 는 struct 사용 할때 더 유용하게 사용 된다. 

```
typedef struct _Person {
    char name[32];
    int age;
} Person;
```
* typedef 키워드 뒤에 struct를 정의 해준다. 

```
struct _Person {
    char name[32];
    int age;
}
```  

* 이 부분이 기존 typedef 에서 기존의 타입 즉, char, int 와 같은 부분을 의미한다.   
* sturct 의 이름은 별명에 사용하기 좋게 하기 위해서 앞에 _ 를 붙여서 구분해주는 것이 좋다.

```
 } Person;
```

 * 이 부분이 struct 정의 부분 전체의 별명이 된다. 

```
Person person = {.name = "김인규", .age = 25};
```

* typedef 를 이용해서 struct 를 정의하면, 위와 같이 sturct 키워드 없이 선언하여 사용 할 수 있다. 
* 그래서 일반적으로 struct 정의는 typedef 를 이용해서 사용 한다. 


[예제 보기](ex/ex01.c)

## struct 배열

* struct 는 배열과 사용해서 사용 성이 배가 된다. 

```
typedef struct _ScoreData {
    char name[32];
    int score;
} ScoreData;
```

```
ScoreData myScores[5];
```
* 위와 같이 일반 배열과 같이 선언해서 사용 할 수 있다. 

```
    ScoreData myScores[5] = {
        {"국어", 90},
        {"수학", 95},
        {"과학", 80},
        {"영어", 100},
        {"사회", 85}
    };
```
* 위와 같이 형태로 초기화가 가능하다. 

```
strcpy(myScores[0].name, "국어");
myScores[0].score = 90;
    
strcpy(myScores[1].name, "수학");
myScores[1].score = 95;
    
strcpy(myScores[2].name, "과학");
myScores[2].score = 80;
    
strcpy(myScores[3].name, "영어");
myScores[3].score = 100;
    
strcpy(myScores[4].name, "사회");
myScores[4].score = 85;
```

* index 를 통해서 하나씩 값을 저장, 변경 할 수 있다. 

```
for(int i = 0; i < 5; i++) {
    printf("%s : %d\n", myScores[i].name, myScores[i].score);
}
```

> 출력 결과

```
국어 : 90
수학 : 95
과학 : 80
영어 : 100
사회 : 85
```
* 다른 배열과 마찬가지로 반복문을 통해서 값을 처리 할 수 있다. 


## struct 동적 할당

```
typedef struct _Person {
    char name[32];
    int age;
} Person;
```

```
Person *myInfo = (Person *)malloc(sizeof(Person));
```
* 다른 타입과 마찬가지 방법으로 malloc 을 통해서 동적 할당을 할 수 있다. 

```
strcpy((*myInfo).name, "김인규");
(*myInfo).age = 25;
    
printf("%s , %d\n", (*myInfo).name, (*myInfo).age);
```
* 동적 할당 특성상 바로 초기화 할수 없고, 값을 직접 저장해 주어야 한다. 

`(*myInfo).age = 25;`

* 포인터 를 통해 접근해야 하기 때문에, 위와 같이 * 를 붙여주어야 한다. 
* 하지만, 빈번하게 사용되기도하고, 가독성도 좋지 못하기 때문에, 더 좋은 방식을 만들어 놓았다. 

```
strcpy(myInfo->name, "김인규");
myInfo->age = 25;
    
printf("%s , %d\n", myInfo->name, myInfo->age);
```
`myInfo->age`

* 위 처럼 * 를 표시하지 않고, . 대신에 **->** 기호를 사용해서 멤버 변수에 접근 할 수 있게 한다. 
* * 를 통해서 접근하는 것보다 훨씬 가독성이 좋다. 

```
Person *persons = (Person *)malloc(sizeof(Person) * 3);
    
strcpy(persons[0].name, "유재석");
persons[0].age = 40;
    
strcpy((persons + 1)->name, "이효리");
(persons + 1)->age = 30;
    
strcpy(persons[2].name, "김인규");
persons[2].age = 20;
```
* 동적 할당을 통해서 배열로 만들어서 사용 할 수 있다. 

`persons[0].age = 40;`

* 배열을 사용 할때는 포인터 참조를 사용 하지 않기 떄문에 일반 배열 사용 처럼 . 을 사용 하면 된다. 

`(persons + 1)->age = 30;`

* 포인터 연산을 통해서 값에 접근 할 경우는 -> 기호를 통해서 접근을 해야 한다.
* struct 의 경우 일반 타입에 비해서 메모리를 많이 사용 하기 때문에, 메모리 낭비가 없도록 각별히 유의 해주어야 한다. 

[예제 보기](ex/ex02.c)
