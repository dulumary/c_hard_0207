# 9. 포인터

## 변수의 주소
* 변수는 메모리에 저장 된다. 
* 변수가 사용 되면, 각각 다른 영역의 메모리 공간이 만들어 지고, 서로 독립되어 관리 된다. 
* 변수가 저장된 메모리에는 주소를 가지고 있다. 
	* 16진수 형태로 이루어져 있다 ex> 0x29AC31
* 변수의 값을 다루는게 일반 적이지만, 변수의 주소를 다루는 경우도 있다. 
* 값을 저장 하기위해 변수를 사용 하듯이, 주소를 저장 하는 변수도 존재한다. 
* 이렇게 주소를 다루는 것을 **포인터(Point)** 라고 하고, 주소를 저장 하는 변수를 **포인터 변수** 라고 한다. 

## 포인터 변수 선언
*  주소를 저장 하는 변수를 선언할 때는 아래와 같이 한다.  
`int *numberPointer;` 
* 변수 처럼 주소를 저장 할때도, 타입을 먼저 정해준다. 
	* 포인터 변수 타입은 저장할 주소의 변수 타입을 의미한다. 
* 변수 이름 앞에 * 를 붙여서 포인터 변수 임을 명시 해준다. 

## 포인터 변수 저장
* 포인터 변수에 주소를 저장 하기 위해서는 일반 변수로 부터 주소를 얻어 와야 한다. 

```
int number = 10;
int* numberPointer = NULL;
    
numberPointer = &number;
```
`numberPointer = &number;`

* 포인터 변수에서 주소를 저장하거나 사용 할때는 *를 제외 하고 변수 이름만 적어 준다. 
* 일반 변수에서 주소를 얻어 낼때 일반 변수 앞에 & 기호를 붙여 준다. 
* numberPointer 변수에 number 의 주소가 저장 되었다. 
* printf 를 통해서 주소를 확인 할 수 있다.   
* 포인터에서 비어 있다는 의미를 표현 하기 위해서 **NULL** 이라는 키워드로 초기화 해준다. 

```
printf("%p\n", numberPointer);
printf("%p\n", &number);
```
* 주소를 출력하는 서식 지정자는 **%p** 이다

> 출력 예시

```
0x7ffeefbff49c
0x7ffeefbff49c
```
* 출력 결과를 보면 정상적으로 저장 된 것을 확인 할 수 있다. 

## 포인터 참조
* 주소 값만으로는 할 수 있는 것이 없다. 
* 주소 값을 통해서 해당 주소에 들어 있는 값을 얻어 낼수 있다.   

`printf("%d\n", *numberPointer);`  

* 포인터 변수에서 해당 주소에 들어 있는 값을 얻기 위해서는 변수 이름앞에 * 를 붙여 준다. 
* 이렇게 주소를 통해서 값을 얻어 내는 것을 **참조** , **reference** 라고 표현한다. 

> 출력 예시   

```
10
```

* 아래 처럼 일반 변수와 포인터 변수를 같은 의미로 표현 할 수 있다. 

> 주소

```
numberPointer == &number
```

> 값

```
*numberPointer == number
```

## 포인터를 통한 값 변경

```
*numberPointer = 30;
```
* 포인터 변수를 통해서도 해당 주소 안에 들어 있는 값을 변경 할 수 있다. 

```
printf("%d\n", *numberPointer);
printf("%d\n", number);
```

> 출력 예시 

```
30 
30
```
* 특이한 점은, 포인터를 통해서 변경 했을 경우, 일반 변수에 들어 있는 값도 변하게 된다. 

```
int number1 = 10;
int number2 = number1;
    
number2 = 30;
    
printf("%d\n", number1);
printf("%d\n", number2);
```

> 출력 예시 

```
10
30
```

* 위 처럼 number1 의 값을 number2 에 넣고, number2 의 값을 변경해도 number1의 값에 영향을 주지 않는다. 
* 그 이유는 number2에는 number1의 값을 저장 할 새로운 메모리 영역을 만들어서 값을 저장 한것 이기 때문에, 둘은 각기 다른 영역에 값이 저장되어 있다. 

```
int number = 10;
int* numberPointer = 0;
    
numberPointer = &number;
```

* 하지만 포인터 변수의 경우 number 의 주소를 저장 한 것이기 때문에, 같은 값을 공유하게 된다. 

`*numberPointer = 30;`

* 따라서 위와 같이 하면 number 가 저장 된 메모리가 공간에 직접 찾아 들어 가서 값을 변경 시키기 때문에 number의 값이 변경 되게 된다. 
* 결국 포인터는 단순히 값을 저장 하는 것이 아니라, 값이 저장된 공간을 관리 하는 방식이다. 
* 이를 통해서, 하나의 공간을 여러 변수를 통해서 관리 하고 이용 할 수 있게 한다. 

## 허상 포인터 (Dangling pointer) 
* 변수는 선언된 블락에서만 유효하고, 블락을 빠져나오면 메모리에서 사라지게 된다. 
* 그럼 이 주소를 가르키고 있던 포인터는 어떻게 될까?

```
int* insidePointer;
if(1) {
    int insideNumber = 5;
    insidePointer = &insideNumber;
    
    printf("%d\n", *insidePointer);
}
    
printf("%d\n", *insidePointer);
```

* if문 안에서 선언된 변수의 주소를 포인터 변수에 저장 한다. 
* 이를 if 문 안에서 사용 하는 경우 아무 문제가 없지만, 밖에서 사용 하려고, 하면 해당 변수는 사라지고 없기 떄문에 가르키는 값이 없어진다. 
* 이렇게 포인터 변수가 참조하는 값이 없어진 상태를 **허상 포인터** 라고 한다. 
* 위와 같이 구현 한경우 컴파일 단계에서 에러가 발생하지는 않지만, 실행 하는 도중에 에러가 발생할 가능성이 높아 진다. 
* 따라서 포인터를 사용 할때는 허상 포인터가 될 여지가 없는지 확실하게 확인해야 한다. 

[예제보기](ex/ex01.c)


## 배열과 포인터 
* 배열은 포인터와 매우 밀접한 관계를 가지고 있다. 
* 사실 우리가 만든 배열은 일반 변수가 아니고 포인터 변수 이다. 
* 선언된 배열을 [0] 와 같은 형태가 아닌 변수 이름 그대로 접근 해보면 어떨까?

```
int numbers[5] = {5, 8, 3, 4, 2};
    
printf("%p\n", numbers);
printf("%d\n", *numbers);
```

> 출력 예시 

```
0x7ffeefbff490
5
```

* 배열 변수 명을 포인터변수 처럼 사용해서 출력 하면 위와 같다. 
*  %p 서식 지정자를  통해서 numbers 의 주소값이 출력 되는 것을 확인 할 수 있다. 
* * 를 통해서 첫번째 값을 가져 오는 것을 확인 할 수 있다. 
* 위 과정을 통해서 numbers 는 포인터 변수 라는 것을 확인 할 수 있다. 
* 결론적으로 numbers 변수는 배열의 가장 첫 번째 값의 주소를 저장 하고 있는 포인터 변수 이다. 

| 0x7ffeefbff490 |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| 
|:---:|:---:|:---:|:---:|:---:|
| [0] | [1] | [2] | [3] | [4] | 
| 5  | 8  | 3  | 4 | 2  | 

## 포인터 변수 연산
* 일반 변수 처럼 포인터 변수도 기본적인 연산이 가능하다. 

```
printf("%p\n", numbers);
printf("%p\n", numbers + 1);
```

> 출력 예시

```
0x7ffeefbff490
0x7ffeefbff494
```

* 포인터 변수에 1을 더하고 주소 값을 확인해 보면 4가 더해진 것을 확인 할 수 있다. 

```
char characters[5] = {'a', 'c', 'e', 'n', 'b'};
    
printf("%p\n", characters);
printf("%p\n", characters + 1);
```

> 출력 예시

```
0x7ffeefbff49b
0x7ffeefbff49c
```
* char 포인터 변수에서 1 을 더하고 주소값을 확인하면 1이 더해진 것을 확인 할 수 있다. 

* 두 가지 예를 통해 확인 할 수 있는 것은 포인터 연산은 해당 타입의 크기 (int : 4byte, char : 1byte) 만큼씩 커지는 것을 확인 할 수 있다. 
* 포인터 연산을 통해서 얻은 새로운 주소를 통해서 값을 얻으면 어떻게 될까?

```
int numbers[5] = {5, 8, 3, 4, 2};

printf("%d\n", *numbers);
printf("%d\n", *(numbers + 1));
printf("%d\n", *(numbers + 2));
```

> 출력 예시

```
5
8
3
```

* numbers 주소 값에 각각 1 과 2를 더한 후 * 를 통해서 해당 값을 참조 하면, 배열에서 각각 [1], [2] 의 값을 가져 오는 것을 볼 수 있다. 
* 즉, 아래와 같이 표현될 수 있다. 

```
*number == numbers[0];
*(number + 1) == numbers[1];
*(number + 2) == numbers[2];
*(number + 3) == numbers[3];
*(number + 4) == numbers[4];
```

* 결국 주소값에 더하기 연산을 한다는 것은 연결된 다음 값의 주소를 의미 하는 것이다. 

| 0x7ffeefbff490 | 0x7ffeefbff494 |0x7ffeefbff498 | 0x7ffeefbff49c | 0x7ffeefbff4a0| 
|:---:|:---:|:---:|:---:|:---:|
| [0] | [1] | [2] | [3] | [4] | 
| 5  | 8  | 3  | 4 | 2  | 

*  주소 값의 연산이 타입마다 결과가 다른 이유는, 데이터의 크기 만큼 주소를 이동해야 다음 값을 얻을 수 있기 때문이다. 

### 주의 사항 

```
printf("%d\n", *(numbers + 1));
printf("%d\n", *numbers + 1);
```
> 출력 예시 

```
8
6
```

* 포인터 연산을 괄호로 묶어 주지 않으면 결과가 틀릴 수 있다. 

`printf("%d\n", *numbers + 1);`  

* 이렇게 표현 할 경우 *numbers 가 먼저 수행되어 numbers[0] 의 값이 구해지고 그 값에 1을 더하게 된다. 

`printf("%d\n", *(numbers + 1));`  

* 따라서, 포인터 연산을 꼭 괄호로 묶어서 수행하고 그 결과에 *를 붙여 주어야 한다. 


## 포인터 대입 연산

```
int* numbersPointer = numbers;
    
printf("%p\n", numbersPointer);
printf("%d\n", *numbersPointer);
    
numbersPointer = numbers + 3;
    
printf("%p\n", numbersPointer);
printf("%d\n", *numbersPointer);
```
* 배열의 포인터 변수를 새로운 포인터 변수에 저장 해서 사용 할 수 있다. 
* 심지어, 포인터 연산을 통해 얻어진 주소를 포인터 변수에 저장해서 사용 할 수 있다. 

> 출력 예시 

```
0x7ffeefbff490
5
0x7ffeefbff49c
4
```

* 이렇게 다양한 방식으로 포인터 변수를 저장해서 관리 할 수 있다. 

[예제보기](ex/ex02.c)