# 0824 #LIVE 강의 필기

# APS(Algorithm Problem Solving)_문자열string

### 목차

- 문자열 : *영어, 한글, 라이브러리 활용*
- **패턴 매칭 : *<u>brute force</u>**, KMP, 보이어-무어*
- 문자열 암호화
- 문자열 압축
- 실습 1, 2

## 문자의 표현

### 컴퓨터에서의 문자 표현

- 글자 A를 메모리에 저장하는 방식 : "A"의 형태를 그대로 비트맵에 저장하지 않는다! 각 문자에 대응되는 **숫자**를 정해 놓고 메모리에 저장한다.
- `ASCHII(American Standard Code for Information Interchange)`
    - 네트워크가 발전하며 각 지역별 코드 체계를 통일해야 한다는 필요성에서 제정된 표준안(1967년)
    - 7bit 인코딩으로 128문자를 표현(0번~127번), 33개의 출력 불가능한 제어문자들과 95개의 출력 가능한 문자들(32번~126번, 공백 포함!)로 이루어짐

    - 1 byte = 영문자 1개를 표현 = 8bit; 나머지 1bit는 error check용 `parity bit`로 활용됨!

- 그 외의 코드 체계 :
    - `BCD` : 6비트; 영어의 대소문자를 합치면 52개이므로, 64가지를 표현할 수 있는 6비트로 표현 가능하다!
    - `EBCDIC` : 8비트
    - `확장 아스키` : 표준 문자 이외의 액센트 문자, 도형 문자, 특수 문자, 특수 기호 등 부가적인 128개 문자를 추가할 수 있는 부호
        - 1byte 내의 8bit를 모두 활용함
        - 컴퓨터 생산자와 소프트웨어 개발자가 여러가지 다양한 문자에 (자의적으로?) 할당할 수 있도록 할 수 있다. 그러나 서로 다른 프로그램 사이에서 교환되지 않으므로 주의할 것!
    - 개별 국가들도 각자의 문자를 표현하기 위한 코드 체계를 갖추고 있으며, **우리나라 역시 조합형/완성형의 두 종류 한글 코드체계**를 가지고 있다! 한글은 2byte

### 유니코드

- 다국어 처리를 위한 표준
- 2 byte = 65.536가지 처리 가능
    - 한글이 11,000자 / 한자 24,000여 자
- **유니코드 Character Set**
    - UCS-2 / UCS-4 : 유니코드를 저장하는 변수의 크기를 정의했으나, 바이트 순서에 대해 표준화하지 못함 → 각 파일이 어떤 캐릭터셋을 쓰는지 인식하고 구분해야 하는 경우 발생
    - **big-endian, little-endian**
        - 큰 단위가 먼저 오는지, 작은 단위가 먼저 오는지 순서가 다르다!
        - 서버는 big-endian, PC는 little-endian 사용
- **유니코드 인코딩** UTF: Unicode Transformation Format
    - UTF-8 (in Web)
        - MIN: 8bit, MAX: 32bit (1Byte *4)
    - UTF-16 (in Window, Java)
        - MIN: 16bit, MAX: 32bit (2Byte *2)
    - UTF-32 (in Linux)
        - MIN: 32bit, MAX: 32bit (4Byte *1)
- **Python 인코딩**
    - **3.x version : 유니코드 UTF-8 (생략 가능)**
        - 다른 인코딩 방식으로 처리 시 첫 줄에서 원하는 인코딩 방식을 지정

---

## 문자열

### 문자열의 분류

- 문자열(string)
    - `fixed length` (고정길이)
    - `variable length` (가변길이)
        - `length controlled` : **java 언어에서의 문자열**, class로 지원
        - `delimited` : **C 언어에서의 문자열**, type이 따로 없음!

### C 언어에서의 문자열

⇒ C에서의 문자열은 **문자들의 배열 형태**로 구현된 응용 자료형이다.

- 문자 배열에 문자열을 저장할 때는 마지막에 끝을 표시하는 널 문자(`\0`)를 입력해, 문자열이 끝났음을 알려줘야 한다.

    ```c
    char arry[] = {'a', 'b', 'c', '\0'};
    ```

    ```c
    char arry[] = "abc";
    ```

- 문자열 처리에 필요한 연산을 함수 형태로 제공한다.
  
    - `strlen()`, `strcpy()`, `strcmp`, ...

### Java(객체지향 언어)에서의 문자열

⇒ 문자열 데이터를 저장, 처리해 주는 클래스를 제공한다.

- String 클래스를 사용한다.

    ```java
    String str="abc"
    ```

    ```java
    String str = new String("abc")
    ```

    - java.lang.String 클래스는 기본적인 객체 메타 데이터와 함께
        - hash값(hash)
        - 문자열의 길이(count)
        - 문자열 데이터의 시작점(offset)
        - 실제 문자열 배열에 대한 참조(value) 네 가지 필드를 포함한다.
- 문자열 처리에 필요한 연산을 연산자, 메소드 형태로 제공한다.
    - `+`, `length()`, `split()`, `substring()`, ...
    - 보다 풍부한 연산 제공

### Python에서의 문자열

⇒ **시퀀스 자료형으로 분류**되며, 텍스트 데이터의 취급 방법이 통일되어 있다.

- **char type 없음** -> 다 string으로 처리
- 문자열 기호
    - `' '`, `" "`, `'''`, `"""`
    - `+` : 연결concatenation)
        - 문자열 + 문자열 ⇒ 이어붙여주는 역할!
    - `*` : 반복
        - 문자열 * 수 ⇒ 수만큼 문자열 반복!
- 문자열 클래스에서 제공되는 메소드
    - `replace()`, `split()`, `isalpha()`, `find()`
- **문자열은 튜플과 같이 요솟값을 변경할 수 없다 (Immutable)!!!!!**

### 문자열 뒤집기 (연습문제1)

- 알고리즘:
    1. 자기 문자열에서 뒤집기
        - swap을 위한 임시 변수가 필요함
        - 반복 수행은 문자열 길이의 반만큼만 수행함
    2. 새로운 빈 문자열을 만들어, 소스의 뒤에서부터 읽어서 새 문자열에 쓰기
- C :  앞선 알고리즘대로 수행!
- java : StringBuffer 클래스의  reverse() 메소드 이용
- Python : Reverse 함수 혹은 slice notaion 이용

    ```python
    s = "Reverse this string"
    s = [::-1]

    		print(s)
    ```

    👉 reverse() 구현하기

    ```python
    # 1) reverse 함수
def str_rev(str):
        # str -> list
        arr = list(str)

        # 반만 돌려줘야 함
        # swap
        for i in range(len(arr)//2):
            arr[i], arr[len(arr)-1-i] = arr[len(arr)-1-i], arr[i]
    
        # list -> str
        str = "".join(arr)
    return str
    
    # ------------------
    str = "algorithm"
    str1 = str_rev(str)
    print(str1)
    # ------------------
    str2 = "algorithm"
    arr2 = list(str2)
    arr2.reverse()
    str2 = "".join(arr2)
    print(str2)
    # ----------------
    # 2. slice notation
    s = "algorithm"
    s = s[::-1]
    print(s)
    ```

### 문자열 비교(compare)

- C : `strcmp()` 함수 제공
- Java : `equals()` 메소드 제공
  
    - 문자열 비교에서 `==` 연산은 메모리 참조가 같은지 묻는것
- Python : `==` 연산자, `is` 연산자 제공
    - `==` 연산자는 내부적으로 특수 메서드 `__eq__()` 호출

    👉 strcmp() 구현하기

    ```python
    def strcmp(s1, s2):
    		i = 0
    		if len(s1) != len(s2):
    				return False
    		else:
    			i = 0                                     # 초기식
    				while i < len(s1) and i < len(s2):      # 조건식
    						if s1[i] != s2[i]
    								return False
    						i += 1                              # 증감식
    		return True

    a = "ABC"
    b = "ABC"

    print(strcmp(a, b)) # True, False
    ```

### 문자열 숫자를 정수로 변환하기

- C : `atoi()` 함수 제공(*Array to Integer*). 역함수로는 `itoa()`
- Java : 숫자 클래스의 parse 메소드 제공
    - 예) `Interger.parseInt(String)`
    - 역함수로는 `toString()`
- Python : 숫자와 문자 변환 함수 제공
    - `int()`, `float()`, `str()`, `repr()`
        - str()은 내용물이 그대로, repr()는 "(따옴표 안에)" 출력된다.

    👉 atoi() 구현하기

    ```python
    def atoi(str):
        value = 0
        for i in range(len(str)):
            c = str[i]
            # 0 ~ 9
            # if c >= '0' and c <= "9":
            if '0' <= c <= '9': # 위에처럼씀, 이건 파이썬만 가능
                digit = ord(c) - ord('0')
                # 파이썬은 c - '0' 안됨
            else:
                break
        value = value * 10 + digit # digit부분  ord(c) - ord('0')만 써도됨(숫자들어온다는 가정)
        return value
    
    a = "123"
    print(type(a))
    b = atoi(a)
    print(type(b))
    ```

### 문자열 교체하기

- 알고리즘 : 교체할 문자열 이후의 문자열을 보관함 → 문자열을 교체한 후 → 보관한 문자열을 덧붙임
- `.replace("원본", "교체")` 로 구현 가능

### 연습문제2 : str() 함수를 사용하지 않고 itoa() 구현

- 양의 정수를 입력 받아 문자열로 변환
- 입력값 : 변환할 정수 값, 변환된 문자열을 저장할 문자 배열
- 반환값 : 없음

```python
def itoa(num):
    x = num    # 몫
    y = 0    # 나머지
    arr = []
    while x:
        y = x % 10
        x = x // 10   # x //= 10
        arr.append(chr(y + ord('0')))

    arr.reverse()
    str = "".join(arr)
    return str


x = 123
print(x, type(x))
str = itoa(x)
print(str, type(str))
```

👉 음수를 변환할 때는 어떤 고려사항이 필요한가요?

---

## 패턴 매칭

### 패턴 매칭에 사용되는 알고리즘들:

- **(고지식한) 패턴 검색 알고리즘 : Brute Force !!!! (구현하기! 중요)**
- 카프-라빈 알고리즘
- KMP 알고리즘
- 보이어-무어 알고리즘

### Brute Force

```python
'''
i(target), j(pattern) N, M이 될 때까지 반복
    반복 종료 후 j == M
    아니면 : 패턴 못찾은 것

두가지 경우에 따라 다르게 제어
    t[i] == p[j] : i와 j를 증가
    t[i] != p[j] : j는 처음으로 i는 현재위치에서 j만큼 빼서 비교 문자로 이동
'''

p = "is"                   # 찾을 패턴
t = "This is a book~!"     # 전체 텍스트
M = len(p)                 # 찾을 패턴의 길이
N = len(t)                 # 전체 텍스트의 길이

def BruteForce(p, t):
    i = 0                  # t의 인덱스 # 문자열 이동 인덱스
    j = 0                  # p의 인덱스
    while j < M and i < N:
        if t[i] != p[j]:  # 매칭에 실패하면
            i = i - j
            j = -1   # 24번 행에서 +1하면 0으로 변경되므로 -> 첫번째 패턴 문자로 이동
            
        i = i + 1
        j = j + 1
        
    if j == M:
        return i - M        # 검색 성공  # 반복 종료 후 j == M이면 : 패턴찾음
    else:
        return -1           # 검색 실패  # 아니면 못찾음 리턴

print(bruteForce(p, t))
```

- 시간복잡도 ⇒ O(mn)
    - 최악의 경우, 시간복잡도는 모든 위치에서의 패턴을 파악해야 하므로
    - 비교 횟수를 줄일 수 있는 방법은 없을까?

        ⇒ KMP 알고리즘의 탄생!

### KMP 알고리즘

- 아이디어 :
    - 불일치가 발생한 텍스트 스트링의 앞 부분에 어떤 문자가 있는지를 미리 알고 있으므로, 불일치가 발생한 앞 부분에 대하여 다시 비교하지 않고 매칭 수행
    - 텍스트에서 abcdabc까지 매치되고, e에서 실패한 상황에서 패턴의 맨 앞 abc와 실패 직전의 abc가 동일함을 이용해보자!
- 패턴을 전처리하여 배열 next[M}을 구해서 잘못된 시작을 최소화함
    - `next[M]`: 불일치가 발생했을 경우 이동할 다음 위치

    💡 `전처리` : 실제로 매턴 매칭을 하기 전, 정보를 미리 계산해두는 것. KMP나 보이어 무어에는 전처리 단계를 거쳐야 한다. 이를 통해 패턴 매칭이 효율적이 된다!

- 시간복잡도 ⇒ O(m+n)

### 보이어-무어 알고리즘

- 대부분의 상용 소프트웨어에서 채택하고 있는 알고리즘!
- 오른쪽에서 왼쪽으로 비교
    - 패턴의 오른쪽 끝에 있는 문자가 불일치하고, 이 문자가 패턴 내에 존재하지 않는 경우

        ⇒ 패턴의 길이만큼 이동할 수 있다! 더 효율적

    - 패턴의 오른쪽 끝에 있는 문자가 불일치하고, 이 문자가 패턴 내에 존재할 경우

        ⇒ 패턴에서 일치하는 문자를 찾아서 점프!

### 연습문제 3

- 고지식한 방법을 이용하여 패턴을 찾아봅시다
- 임의의 본문 문자열과 찾을 패턴 문자열을 만듭니다
- 결과 값으로 찾은 위치 값을 결과로 출력합니다

```python
def brute(t, p):
    i, j = 0, 0
    while j < len(p) and i < len(t):
        if t[i] != p[j] :
            i = i - j
            j = -1
        i += 1
        j += 1
    if j == len(p) :
        return i - len(p)
    else:
        return -1

text = "TTTTTAACCA"
pattern = "TTA"

print(brute(text, pattern))
# 밑에꺼 쓰면 한번에 되긴 함
print(text.find(pattern))
```

- 참고 : `find()`

    ```python
    print(text.find(pattern))
    ```