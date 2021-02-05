# 10. 포인터 응용

## 함수 파라미터와 포인터
```
void foo(int x) {
    x += 5;
}

int main(int argc, const char * argv[]) {

    int number = 10;
    foo(number);
    printf("%d\n", number);
}
```

* 파라미터로 넘긴후 함수내에서 값을 변경하면, number의 값은 어떻게 될까?

> 출력 결과

```
10
```

* 결과는 number에 변화가 없이 그대로이다. 
* 파라미터로 넘긴 변수는 변수 자체를 넘긴게 아니라 값만 전달 될것이다. 
* 즉, 전달된 값은 함수내에서 새로운 메모리에 저장이 되고, number 와 함수 내의 x는 전혀 관련이 없다. 
* 이를 통해서, 파라미터로 넘긴 변수의 안정성이 확보 된다. 
* 이런 형태로 함수에 파라미터를 넘기를 것을 값을 통해 함수를 호출한다고 하여, **Call by Value** 라고 한다. 

## 변화되는 파라미터
* Call by Value 형태의 호출이 가장 일반 적이지만, 용도에 따라서 전달한 변수의 값을 함수 내에서 직접 변경 시킬 수도 있다. 

```
void foo2(int* x) {
    *x += 5;
}
int main(int argc, const char * argv[]) {

    int number = 10;
    int* numberPointer = &number;
    foo2(numberPointer);
    printf("%d\n", number);
  
}
```

`void foo2(int* x) `  

* 파리미터를 포인터 형태로 받는다. 
* 이를 통해서, 해당 값을 받는 것이 아니라, 값이 저장되어 있는 주소를 받을 수 있다. 
* 주소를 통해서 참조하면, 해당 값을 공유하게 되어 변수값을 변경 할 수 있게 된다. 

`*x += 5;`

* 전달된 파라미터가 포인터 변수이기 때문에 값을 변경하기 위해서 * 를 이용해 참조한다.  

```
int* numberPointer = &number;
foo2(numberPointer);
```

* 파라미터로 포인터 변수를 넘기기 위해서 number 의 주소를 저장 하고 이를 파라미터로 넘기게 된다. 

> 출력 결과 

```
15
```
* 변수의 주소를 전달하여, 변수 값을 공유하고 이를 통해서 5가 증가된 15를 얻게 된다.
* 이렇게 포인터를 응용해서 함수내에서 외부에서 전달된 변수 값을 변경 할 수 있다.
* 이러한 형태를, 참조를 통해서 함수를 호출 한다고하여, **Call by Reference** 라고 한다. 

## 배열 파라미터

```
void arrayParameter(int array[], int size)  {
    
    for(int i = 0; i < size; i++) {
        printf("%d ", array[i]);
    }
    printf("\n");
}

int main(int argc, const char * argv[]) {
    int numbers[5] = {1, 2, 3, 4, 5};
    arrayParameter(numbers, 5);
    return 0;
}
```
`void arrayParameter(int array[]) ` 

* 파라미터 이름 뒤에 [] 를 붙여 주면, 배열을 파라미터로 전달 할 수 있다. 
* 배열의 변수는 포인터 변수이기 때문에 배열 파라미터는 Call by Reference 의 형태이다. 
* 따라서 전달되는 배열의 값은 변경이 가능하다. 
* 배열은 포인터 기반이기 때문에 Call by Value 형태로 파라미터 사용이 불가능하다. 
* 배열을 파라미터로 받을 때는 배열 길이도 같이 받아서, 이를 통해서 반복을 수행하는 것이 좋다.

`void arrayParameter(int* array)`  

* 배열은 걸국 포인터 변수 이기 떄문에 위와 같은 형태로도 전달 받을 수 있다. 

[예제 보기](ex/ex01.c)

## 문자열과 포인터

* 문자열은 char 배열의 특수한 형태의 변수이다. 
* 배열이 기반이기 때문에, 포인터를 통한 이용도 가능해진다. 

`char string[] = "Hello";`  
`char* string = "Hello Wrold!!";`

* string 을 배열 형태가 아닌 포인터 변수 형태로 바로 초기화 할 수 있다. 
* 선언은 포인터로 했지만, 내부적인 형태는 배열의 구조를 가지고 있다. 
* 단, `char string[] ` 형태의 선언은 문자열 내부의 문자를 수정 할 수 있지만,  `char* string` 형태의 선언은 추후에 문자열내의 문자를 수정 할 수 없다. 

```
printf("%s\n", string);
char *world = string + 6;
printf("%s\n", world);
```

> 출력 결과

```
Hello World!!
World!!
```

* 포인터 연산을 통해서 지정한 위치에서 부터 출력 하도록 할 수 있다. 
* 포인터는 지금 가르키고 있는 주소 부터 시작이라고 인식 하기 떄문에, 이러한 표현이 가능하다. 

## 포인터를 이용한 문자열 함수 

* 포인터를 활용한 좀 더 활용도 높은 함수들이 존재 한다. 
* string.h 에 포함되어 있어서 사용하기 위해서는 `#include<string.h>` 를 포함해 주어야 한다.

| 함수 원형                          | 기능 |
|---------------------------------------------------------|--------------|
| char * **strcpy** ( char * destination, const char * source );   | 문자열을 복사해준다.   |
| char * **strncpy** ( char * destination, const char * source, size_t num );   | 문자열을  특정 길이 만큼 복사해준다.   |
| char * **strstr** ( const char * str1, const char * str2 );     |  문자열 내에서 다른 문자열이 있는 위치를 반환해준다  |
| char * **strtok** ( char * str, const char * delimiters );    |  문자열 내에서 특정 문자열을 기준으로 문자열을 잘라준다.  |


### strcpy
* 첫번째 파라미터로 받은 char 배열에, 두번째 파라미터로 받은 문자열을 복사 한다. 

```
char* string = "Hello World!!";
  
char string1[128];
    
strcpy(string1, string);
printf("%s\n", string1);

strcpy(string1, "cooooool");
printf("%s\n", string1);
```

> 출력 결과

```
Hello World!!
cooooool
```

### strncpy
* 첫번째 파라미터로 받은 char 배열에, 두번째 파라미터로 받은 문자열을 세번째 파라미터 길이 만큼 복사 한다. 

```
char copynString[128];
strncpy(copynString, string, 5);
printf("%s\n", copynString);
    
strcpy(copynString, string);
printf("%s\n", copynString);
    
strncpy(copynString + 6, "Korea", 5);
printf("%s\n", copynString);
```

> 출력 결과

```
Hello
Hello World!!
Hello Korea!!
```

* 첫 번째 파라미터에는 저장 할 공간이 필요 하기 때문에, 변수로 선언하고 충분한 크기로 만들어 주어야 한다. 
* 파라미터로 문자열을 직접 넘기는 것 또한 가능하다. 

### strstr
* 첫번째 파라미터로 받은 문자열에서 두번째 파라미터로 받은 문자열이 포함되어 있는지 확인한다. 
* 문자열이 포함되어 있으면, 그 시작점의 주소를 포인터 변수로 리턴한다. 
* 문자열이 포함되어 있지 않으면 NULL 을 리턴한다. 

```
char* string = "Hello World!!";

char *string2 = strstr(string, "World");
printf("%s\n", string2);
```
> 출력 결과 

```
World!!
```

*  문자열에서 World 를 찾고 그 위치를 리턴 받을 수 있다. 
*  리턴 받은 포인터 변수를 그대로 출력 하면 그 위치 부터의 문자열을 확인 할 수 있다. 

### strtok
* 첫번쨰 파라미터로 전달 받은 문자열을 두번째 파라미터로 받은 문자열을 기준으로 잘라 준다. 

```
char longString[] = "Fire in the hole";
    
char* word = strtok(longString, " ");
while (word != NULL) {
    printf("%s\n", word);
    word = strtok(NULL, " ");
}
```

`char longString[] = "Fire in the hole";`

* strtok 함수가 내부적으로 해당 문자열을 수정 하므로 배열의 형태로 선언 해주어야 한다. 

`char* word = strtok(longString, " ");`

* 대상이 되는 문자열과 자를 문자열을 차례로 넣어 준다. 
* 해당 함수는 한번에 모든 문자열을 자르는것이 아니라, 반복문을 통해서 순차적으로 하나씩 잘라 준다. 
* 리턴되는 포인터는 자를 문자열의 위치가 순서대로 리턴된다. 
 
`while (word != NULL) `  

* 더 이상 자를 문자열이 없으면 NULL이 리턴된다. 
* 이를 이용해서, NULL 이 아닐 동안 while 을 통해 반복 한다. 

`word = strtok(NULL, " ");`  
 
 *  한번에 다 처리 되지 않기 때문에 while 안에서 반복해서 strtok 을 호출 해주어야 한다. 
 *  반복문 안에서는 첫번째 파라미터를 NULL 로 넣어 주어야 이어서 자르는 과정을 수행한다. 
 *  첫번째 파라미터에 문자열을 넣으면 처음부터 다시 시작하게 된다. 

 > 출력 결과 
 
 ```
Fire
in
the
hole
 ```

[예제 보기](ex/ex02.c)