# hello my first python 🐍

<br>

```
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!


아름다움이 추함보다 낫다.
명시적인 것이 암시적인 것보다 낫다.
단순함이 복잡함보다 낫다.
복잡함이 난해함보다 낫다.
평평한 것이 중첩된 것보다 낫다.
드문드문한 것이 밀집된 것보다 낫다.
가독성은 중요하다.
특별한 경우는 규칙을 깨뜨릴 만큼 특별하지 않다.
비록 실용성이 순수성보다 우선하지만.
에러는 절대 조용히 지나가면 안된다.
명시적으로 조용히 처리되지 않는 한.
모호함에 직면했을 때, 추측하는 유혹을 거부하라.
분명하고, 가능하면 하나의 명확한 방법이 있어야 한다.
그 방법이 처음에는 분명하지 않을 수 있지만, 당신이 네덜란드인이라면 분명할 것이다.
지금이 결코보다 낫다.
하지만 결코가 종종 *지금 당장*보다는 낫다.
만약 구현을 설명하기 어렵다면, 그건 나쁜 아이디어다.
만약 구현을 설명하기 쉽다면, 그건 좋은 아이디어일 수 있다.
네임스페이스는 정말 훌륭한 아이디어다 – 더 많이 사용하자!

```

<br>


## 📌 01. 파이썬 데이터 모델 

#### 👉 파이썬 데이터 모델

> - 파이썬의 최고의 장점은 '일관성'. 이를 통해 새로운 기능에 대해서도 제대로 예측 가능함
> - 데이터 모델은 일종의 프레임워크로서, 파이썬을 설명하는 것이라고 생각할 수 있음
> - 시퀀스, 반복자, 함수, 클래스, 콘텍스트 관리자 등 언어 자체의 구성단위에 대한 인터페이스를 공식적으로 정의함
> - 파이썬 인터프리터는 특별 메서드를 호출해서 기본적인 객체 연산을 수행하는데, 종종 특별한 구문에 의해 호출됨
>   - 예를 들어서, obj[key] 형태의 구문은 `__getitem()__` 특별 멧드가 지원함.
>   - my_collection[key]를 평가하기 위해 인터프리터는 my_collection.__getitem__(key)를 호출함
> - 이처럼 특별 메서드는 우리가 구현한 객체가 다음과 같이 기본적인 언어 구조체를 구현하고 지원하고 함께 사용할 수 있게 해줌
>   - (1) 반복, (2) 컬렉션, (3) 속성 접근, (4) 연산자 오버로딩, (5) 함수 및 메서드 호출, (6) 객체 생성 및 제거, (7) 문자열 표현 및 포맷, (8) 블록 등 콘텍스트 관리

<br>

#### 👉 파이썬 카드 한 벌

```python
import collections

# 간단한 클래스 표현
Card = collections.namedtuple('Card', ['rank', 'suit'])

class FrenchDeck :
  # cv 정의(공통 속성)  
  ranks = [str(n) for n in range(2, 11)] + list('JQKA')
  suits = 'spades diamonds clubs hearts'.split()

  # 초기화 메서드(특별 메서드)
  def __init__(self) :
    # iv 정의(개별 속성)
    # - 1. '변수명' : 외부에서 접근 가능
    # - 2. 'self._변수명' : 내부에서만 사용하도록 단순 언더 스코어(_) 사용. 즉, 작성자가 해당 iv는 비공개로 사용하려는 의도(접근 제어 관례)
    self._cards = [Card(rank, suit) for suit in self.suits
                                    for rank in self.ranks]

  # 길이 반환 메서드(특별 메서드)
  def __len__(self) :
     return len(self._cards)

  # 인덱스의 값 접근하는 메서드(특별 메서드) 
  def __getitem__(self, position) :
     return self._cards[position]

```

> - 위의 코드를 살펴보자
> - collections.namedtuple()을 이용해서 개별 카드를 나타내는 클래스를 간단하게 표현함
> - FrenchDeck 클래스는 간단하지만 아무 많은 기능을 구현함. 파이썬의 특징과 특별 메서드를 통해 파이썬 데이터 모델을 사용할 때의 이점을 파악
>   - (1) 사용자는 클래스 자체에서 구현한 임의의 메서드명을 인지할 필요없음
>   - (2) 파이썬 표준 라이브러리에서 제공하는 풍부한 기능을 별도로 구현할 필요 없리 바로 사용할 수 있음
>   - (3) 한 특별 메서드에 의해 여러 기능을 사용할 수 도 있음. 예를 들어서 `__getitem__()`을 통해 '슬라이싱, 인덱스 접근'과 '반복 처리'를 사용 가능
> - <strong>FrenchDeck이 암묵적으로 object를 상속받지만 상속 대신 데이터 모델과 구성을 이용해서 기능을 가져옴</strong>
> - <strong>`__len__()`과 `__getitem__()` 특별 메서드를 구현함으로써 FrenchDeck을 표준 "파이썬 시퀀스"처럼 작동하므로 반복 및 슬라이싱 등의 핵심 언어 기능 및 random의 choice(), reversed(), ... 라이브러리를 사용할 수 있음</strong> 

<br>

#### 👉 특별 메서드는 어떻게 사용되나?

> - 특별 메서드는 파이썬 인터프리터가 호출하기 위한 것. 우리의 소스 코드에서는 len(my_object) 형태를 호출하면 파이썬 인터프리터는 우리가 구현한 `__len__()` 객체 메서드를 호출하는 원리
> - 그러나 list, str, bytearray 등과 같은 내장 자료형의 경우, 파이썬 인터프리터는 손쉬운 방법을 선택함
> - 예를 들어서 for i in x : 문의 경우 실제로는 iter(x)를 호출하며, 이 함수는 `x.__iter__()` 호출하는 구조임
> - 그렇기에 사용자 코드에서 특별 메서드를 직접 호출하는 경우는 많지 않음
> - 특별 메서드를 호출해야 하는 경우, 일반적으로 len(), iter(), str() 등 관련된 내장 함수를 호출하는 것이 좋음
> - 이들 내장 함수가 해당 특별 메서드를 호출함. 하지만 내장 데이터형의 경우 특별 메서드를 호출하지 않는 경우도 있으며 메서드 호출보다 빠름

<br>


#### 👉 수치형 흉내 내기(유클리드 벡터 구현)

<br>

<img src="https://github.com/user-attachments/assets/c7db3791-9282-4ff7-8ebd-a657f3d455ab" width="500" height="500"/>

<br>

```python

from math import hypot

class Vector :
  def __init__(self, x=0, y=0) :
    self.x = x
    self.y = y

  def __repr__(self) :
    return 'Vector(%r, %r)' % (self.x, self.y)

  def __abs__(self) :
    return hypot(self.x, self.y)

  def __bool__(self) :
    return bool(abs(self))

  def __add__(self, other) :
    x = self.x + other.x
    y = self.y + other.y
    return Vector(x, y)

  def __mul__(self, scalar) :
    return Vector(self.x * scalar, self.y * scalar)

# 사용 예시
v1 = Vector(2, 4)
v2 = Vector(2, 1)
v1 + v2

# >> Vector(4, 5)

v = Vector(3, 4)
abs(v)

# >> 5.0

v * 3
# >> Vector(9, 12)

abs(v * 3)
# >> 15.0
```
> - 위 예시에서 눈여겨 봐야할 것은
> - 우리가 실질적으로 `__init__()`을 제외하고 5개의 특별 메서드를 구현했지만, 이 메서드들은 클래스 내부나 콘솔의 테스트 코드에서 직접 호출하지 않음
> - 즉, 특별 메서드는 주로 파이썬 인터프리터가 호출함

<br>

#### 👉 문자열 표현 

> - `__repr__()`는 객체를 문자열로 표현하기 위해 repr() 내장 메서드에 의해 호출됨
> - 해당 메서드를 구현하지 않을 경우 <Vector object at 0x10e100070> 형식으로 출력됨
> - `__repr__()` 메서드에서는 출력할 속성의 표준 표현을 가져오기 위해 '%r'을 사용함. 이는 좋은 습관
> - `__repr__()` 메서드가 반환한 문자열은 명확해야 하며, 가능하면 표현된 객체를 재생성하는 데 필요한 소스 코드와 일치해야함
> - `__repr__()`과 `__str__()`을 비교해 보면, `__str__()`의 경우 str() 생성자에 의해 호출되며 print()에 의해 암묵적으로 사용됨
> - `__str__()`은 사용자에게 보여주기 적당한 형태의 문자열을 반환함
> - <strong>파이썬 인터프리터는 `__str__()`이 구현되어 있지 않을 때의 대책으로 `__repr__()`를 호출함</strong>


<br>

#### 👉 산술 연산자

> - Vector 클래스로 부터 생성된 인스턴스가 '+', '*' 를 사용하는 경우
> - `__add__()`, `__mul__()`이 각 각 호출됨
> - 또한, 위의 코드를 보면 iv를 변경하는 것이 아닌 새로운 오브젝트를 생성해서 반환하는 불변 형식이 사용된 것을 확인할 수 있음



<br>

#### 👉 사용자 정의형의 불리언 값

> - '참된' 값인지 '거짓된' 값인지 판단하기 위해 파이썬은 bool(x)를 적용함. 해당 함수는 항상 True/False를 반환함
> - `__bool__()`이나 `__len__()`을 구현하지 않은 경우, 기본적으로 사용자 정의 클래스의 객체는 True
> - <strong>bool(x)는 x.`__bool()__`을 호출한 결과를 이용함. `__bool__()`이 구현되어 있지 않으면 파이썬은 x.`__len__()`을 호출하며, 이 특별 메서드가 0을 반환하면 bool()은 False를, 그렇지 않으면 True를 반환함</strong>

<br>

#### 👉 특별 메서드 개요

| 범주                   | 메서드 명                                                                 |
|------------------------|---------------------------------------------------------------------------|
| 객체 생성 및 소멸         | `__new__`, `__init__`, `__del__`                                         |
| 문자열 표현              | `__repr__`, `__str__`, `__format__`, `__bytes__`                          |
| 숫자형 연산              | `__abs__`, `__add__`, `__and__`, `__floordiv__`, `__mod__`, `__mul__`, `__neg__`, `__or__`, `__pow__`, `__radd__`, `__rand__`, `__rfloordiv__`, `__rmod__`, `__rmul__`, `__ror__`, `__rpow__`, `__rsub__`, `__rtruediv__`, `__sub__`, `__truediv__`, `__xor__` |
| 타입 변환 및 캐스팅        | `__bool__`, `__complex__`, `__int__`, `__float__`, `__index__`, `__round__`, `__trunc__` |
| 비교 연산               | `__eq__`, `__ge__`, `__gt__`, `__le__`, `__lt__`, `__ne__`                |
| 컨테이너                | `__contains__`, `__getitem__`, `__setitem__`, `__delitem__`, `__len__`, `__iter__`, `__reversed__`, `__missing__` |
| 속성 접근 및 관리        | `__getattr__`, `__getattribute__`, `__setattr__`, `__delattr__`, `__dir__`|
| 호출 가능성              | `__call__`                                                               |
| 컨텍스트 관리            | `__enter__`, `__exit__`                                                  |
| 속성 관리자              | `__get__`, `__set__`, `__delete__`                                        |
| 객체 복사 및 딥카피       | `__copy__`, `__deepcopy__`                                                |
| 임시 객체                | `__slots__`                                                              |
| 매직 메서드              | `__dict__`, `__class__`, `__doc__`, `__module__`, `__weakref__`            |
| 클래스 관련               | `__bases__`, `__subclasshook__`, `__init_subclass__`, `__prepare__`        |
| 오버로딩                | `__instancecheck__`, `__subclasscheck__`                                   |
| 수명주기                | `__enter__`, `__exit__`, `__del__`                                         |


<br>

#### 👉 왜 len()은 메서드가 아닐까?

> - '파이썬 선'에서 <strong>실용성이 순수성에 우선한다.</strong>라는 말이 있음
> - len(x)는 x가 내장형의 객체일 때 빨리 실행됨. CPython의 내장 객체에 대해서는 메서드를 호출하지 않고 단지 C언어 구조체의 필드를 읽어올 뿐임
> - 컬렉션에 들어 있는 항목 수를 가져오는 연산은 자주 발생하기에 str, list, memoryview 등의 다양한 기본형 객체에 대해 효율적으로 작동해야함
> - 즉, len()은 abs()와 마찬가지로 파이썬 데이터 모델에서 특별한 대우를 받으므로 메서드라고 부르지 않음
> - 물론 `__len__()` 특별 메서드 덕분에 내가 정의한 객체에서 len() 메서드를 직접 정의할 수 있음

<br>

#### 👉 요약 

> - <strong>특별 메서드를 구현하면 사용자 정의 갹체도 내장형 객체처럼 작동하게 되어 '파이썬스러운' 표현력 있는 코딩 스타일을 구사할 수 있음</strong>
> - 파이썬 객체는 기본적으로 자신을 문자열 형태로 제공함
>   - (1) 디버깅 및 로그에 사용하는 형태 : `__repr__()`
>   - (2) 사용자에게 보여주기 위한 형태 : `__str__()`
>
> - 파이썬 객체를 시퀀스로 활용하기 위해 사용하는 특별 메서드들도 있었음
>   - (1) 특정 인덱스 원소 조회 : `__getitem__()`
>   - (2) 객체 길이 반환 : `__len__()`
>   
> - 파이썬 객체를 해당 객체에 맞는 연산자 오버로딩도 처리함
>   - (1) + : `__add__()`
>   - (2) * : `__mul__()`


### 0. 특별 메서드는 왜 존재할까?

- 파이썬과 자바의 차이점 : 인터페이스의 유무
  - 인터페이스는 "약손, 표준화"를 의미 -> 미리 약속된 것으로 프로그래밍함
- 파이썬에서는 "특별 메서드" 제공 : 미리 약속된 메서드로서 인터페이스를 대체함
- "특별 메서드"를 통해 파이썬 내부 동작 수정 가능
  - 파이썬 프레임워크나 라이브러리는 모두 클래스의 특별 메서드를 기반으로 처리됨
- 데이터 모델? : 컬렉션 프레임워크(표준화) - 사용자입장에서 쉽게 쓰기 위함(공통적으로 처리)
- Iterator? : 조건식을 분리함, 사용하는 쪽에서 구현하는 쪽으로 이동
  - for i in x : ~~
    - 내부적으로 iter(x), x.__iter__() 호출함
      - 해당 특별 메서드에 "조건식" 존재함
      

<br>

### 1. 동적 언어(스크립트 언어)의 장점

- 매우 유연함. 예를들어서, iterator에서 반복처리 하려는데 내부에 __next__() 메서드가 없어서 에러가 뜰 경우, 동적으로 __next__()를 추가할 수 있음
- <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/28faac45-455b-43ab-897e-dd80b350eff0">
- 또한, 파이썬의 경우 피연산자의 순서가 바뀌었을 때는 (a * b -> b * a) 역순 연산자가 사용됨

<br>

### 2. 파이썬과 자바의 '상속' 차이
- 파이썬에서 '상속'이란?
  - 파이썬에서는 클래스 계층 구조에 따라 메서드와 속성에 접근. 즉, 코드가 합쳐지는 것이 아님
  - 파이썬 상속 체계에서 기본적으로 모든 클래스가 object 클래스를 기반함
    - (1) 일관된 클래스 구조 => 기본 구조 & 메서드
    - (2) 공통 기능 제공 => __str__(), __repr__() __eq__(), __hash__() ...
    - (3) 다형성

- 파이썬 '상속' vs 자바 '상속'
  - (1) 기본 클래스 => object/Object, 명시적으로 정의하는 방법이 다름
  - (2) 다중 상속 => 파이썬은 다중 상속 가능, 자바는 단일 상속
  - (3) MRO => MRO? '메서드 해석 순서', 클래스 계층 구조에서 메서드를 찾음, 파이썬은 다중 상속 구조/자바는 단일 상속 구조
  - (4) 인터페이스와 믹스인 : 파이썬에서 '믹스인'을 통해 n개 기능 조합, 자바에서는 인터페이스를 통한 다중 구현

<br>

### 3. 파이썬과 자바의 '모듈' 차이
- 파이썬 '모듈' vs 자바 '모듈'
  - 파이썬의 경우, 모듈은 파일을 의미함. 자바의 경우, 모듈은 패키지
    - module, component, class 모두 묶는 개념, 범위가 서로 상이할 뿐
  - 필요할 시 import 해서 모듈을 댕겨옴. 즉, 자신의 네임 스페이스(globals())에 댕겨온 모듈의 네임 스페이스를 등록함
    - 모든 스코프에는 네임 스페이스가 있음. 네임 스페이스는 Map
  - 특정 이름을 찾으면 자신의 네임 스페이스부터 탐색, 그 이후에도 없으면 등록된 네임 스페이스 탐색, 없으면 NameError 발생 

<br>

### 4. 파이썬에서 '오버로딩'과 '오버라이딩'이 적용될까?


<img src="https://github.com/user-attachments/assets/2d815752-1d1b-49b9-b92e-e9a56fbda5b7" width="500" height="500"/>

- 오버로딩이란?
- "같은 이름의 메서드를 여러개 정의하는 것"
  - (1) 메서드 이름이 같아야함
  - (2) 매개변수의 개수 및 타입이 달라야함
  - (3) 반환 타입 상관없음 


- 오버라이딩이란?
- "조상의 메서드를 자손에서 재정의하는 것"
  - (1) 메서드의 선언부가 일치해야함
  - (2) 자손에서 조상 보다 접근 제한자가 좁으면 안됨
  - (3) 자손에서 조상보다 더 큰 범위의 예외를 선언할 수 없음

- 결론, 파이썬에서는 오버로딩이 불가능하며 오버라이딩은 가능함


<br>

### 5. 파이썬에서는 접근 제한자를 어떻게 쓸까??

- 파이썬에서는 엄격한 접근 제한자를 지원하지 않음
  - 관례에 따라 접근성을 나타냄. 즉, 강제하는 문법이 아님 

- 크게 3가지가 있음
  - (1) public : 공개
  - (2) protected : 보호, '_' 단일 언더스코어 사용, 해당 멤버가 클래스 내부와 서브클래스에서만 접근 가능해야 한다는 것을 나타냄
  - (3) private : 비공개, '__' 이중 언더스코어 사용, 해당 멤버가 내부에서만 접근 가능함을 의미함

<br>

### 6. 파이썬에서 iv, cv는 어떻게 선언할까?

- 클래스 내부 영역에 선언되는 변수는 cv
- 생성자(__init__())에 self.name 과 같이 선언되는 변수는 iv
- 파이썬에서는 메서드가 3개
  - (1) 인스턴스 메서드
  - (2) 스태틱 메서드
  - (3) 클래스 메서드
 
<br>

### 7. 파이썬에서 전역 스코프에 함수를 정의한다?

- 이는 전연 스코프에 네임 스페이스에 해당 함수를 등록함
- 즉, Flyweight 패턴이 적용됨

<br>

### 8. 자바와 파이썬에서의 디자인 패턴 구현의 차이

- 파이썬은 매우 간단하며 유연함
  - (1) 파이썬에서는 전략 패턴과 같은 단일 메서드 인터페이스를 클래스로 구현하는 것이 아닌 함수로 정의하면됨
  - (2) 동적으로 실행 중에 선택해서 넣기가 편리함
    - 예를들어서, 할인 정책 함수 객체 중에 할인가가 최대 값이 나오는 함수 객체를 동적으로 선택할 수 있음
    - 이때 중요한 개념이 '모듈'과 '네임 스페이스'

<br>

### 9. 데커레이터 & 클로저

<img src="https://github.com/user-attachments/assets/1906dafc-277e-47ec-9277-93710a3e20d7" width="500" height="500"/>

- 데커레이터 팩토리 : 호출되면 대상 함수에 적용할 실제 데커레이터를 반환
- 데커레이터를 만들기위한 헬퍼
  - 1. functools.lru_caached()
    - 메모이 제이션 구현(캐싱)
  - 2. functools.singledispatch()
    - 범용 함수 선언, 특호된 함수를 시스템 어디에나 어느 모듈이나 등록 가능 

<br>

### 10. 파이썬 iv 캡슐화 및 보호 ...

- __getattr__() : getter, 프로퍼티
- __setattr__() : setter, 프로퍼티
  - 객체의 동작의 불일치를 피하려면 둘 다 동시에 구현해야함
  - __setattr__() 을 통해 프로퍼티(iv)를 read-only로 제한할 수 있음
 
- reduce(<함수>, <반복형>, <초기값>) : 누적합 ... 처리
- zip() : 각 반복형에서 나온 항목들을 튜플로 묶어서 두 개 이상의 반복형을 병렬로 반복하기 쉽게해줌

<br>

### 11. 파이썬스러운 객체

```python
from array import array
import numbers
import reprlib
import math
import numbers
import functools
import operator
import itertools  # <1>

"""
Python의 Vector 제대로 구현한 형태 
- 이거 스스로 만들 줄 알아야함 

핵심 포인트
- (1) __getitem__()과 __len__() 구현 -> 시퀀스처럼 동작할 수 있게 만듦
- (2) __getattr__() 구현 -> read-only로 접근하도록 만듦
- (3) __setattr__() 구현해서 객체 동작의 불일치 피하기 위함 -> __getattr__() & __setattr__() 동시에 구현
    - 단일 문자 속성에 값을 할당하지 못하게 막음 e.g vector.x = 10 오류 발생
- (4) __hash__() 구현할 때 functools.reduce()를 사용
"""

class Vector:
    typecode = 'd'

    def __init__(self, components):
        self._components = array(self.typecode, components)
        res = self._components is components

    def __iter__(self):
        return iter(self._components)

    def __repr__(self):
        components = reprlib.repr(self._components)
        components = components[components.find('['):-1]
        return 'Vector({})'.format(components)

    def __str__(self):
        return str(tuple(self))

    def __bytes__(self):
        return (bytes([ord(self.typecode)]) +
                bytes(self._components))

    def __eq__(self, other):
        if isinstance(other, Vector) : 
            return (len(self) == len(other) and
                all(a == b for a, b in zip(self, other)))
        else : 
            return NotImplemented
        
    def __ne__(self, other) : 
        eq_result = self == other
        
        if eq_result is NotImplemented : 
            return NotImplemented
        
        else : 
            return not eq_result

    def __hash__(self):
        hashes = (hash(x) for x in self)
        return functools.reduce(operator.xor, hashes, 0)

    def __abs__(self): 
        """객체의 절대값을 반환하는 함수"""
        return math.sqrt(sum(x * x for x in self))
    
    def __neg__(self) : 
        """ 단항 연산자 오버라이딩 : -x """
        return Vector(-x for x in self)
    
    def __pos__(self) : 
        """ 단항 연산자 오버라이딩 : +x """
        return Vector(self)
    
    def __add__(self, other) : 
        """ 
        덧셈 연산자 오버라이딩 : x + y 
        
        - TypeError -> NotImplemented : __add__()와 __radd__() 메서드를 구현해서 + 연산자를 안전하게 오버로드함
        """
        try : 
            pairs = itertools.zip_longest(self, other, fillvalue = 0.0)
            return Vector(a + b for a, b in pairs) # 불변 처리, 항상 새로운 인스턴스 생성 
        except TypeError : 
            return NotImplemented # 파이썬이 __add__() 에러 나고 __radd__() 호출할 수 있게 만듦
    
    def __radd__(self, other) :
        """ __add__()로 위임 """
        return self + other

    def __mul__(self, scalar) : 
        if isinstance(scalar, numbers.Real) : # 자료형 검사 
            return Vector(n * scalar for n in self)
        else : 
            return NotImplemented
    
    def __rmul__(self, scalar) : 
        return self * scalar
    
    def __matmul__(self, other) : 
        """
        @ 연산자는 '행렬 곱셉'을 나타남
        - a @ b 는 a 행렬과 b 행렬의 내적을 나타냄 
        """
        try : 
            return sum(a * b for a, b in zip(self, other))
        except TypeError : 
            return NotImplemented
        
    def __rmatmul__(self, other) : 
        return self @ other
    
    def __bool__(self):
        return bool(abs(self))

    def __len__(self):
        return len(self._components)

    def __getitem__(self, index):
        cls = type(self)
        if isinstance(index, slice):
            return cls(self._components[index])
        elif isinstance(index, numbers.Integral):
            return self._components[index]
        else:
            msg = '{.__name__} indices must be integers'
            raise TypeError(msg.format(cls))

    shortcut_names = 'xyzt'

    def __getattr__(self, name):
        """
        객체의 속성을 가져올 때 호출, 객체에 존재하지 않는 속성에 접근하려고 할 때
        자동으로 호출됨. 존재하는 속성에 접근할 때는 호출되지 않음
        
        # 용도
        - 동적 속성 : 객체의 속성을 동적으로 생성하거나 변경
        - 디폴트 값 : 객체에 특정 속성이 없을 때 디폴트 값 제공 가능 
        - 프로퍼티 접근 로깅 : 속성 접근을 로깅하거나 디버깅할 때 활용
        
        # 차이
        - __getattribute__() : 존재하는/존재하지 않는 속성 접근에 대해 호출. 해당 메서드는 모든 속성 접근을 오버라이드함
        - __setattr__() : 객체의 속성을 설정할 때 호출함 
        - __delattr__() : 객체의 속성을 삭제할 때 호출함 
        
        """
        cls = type(self)
        if len(name) == 1:
            pos = cls.shortcut_names.find(name)
            if 0 <= pos < len(self._components):
                return self._components[pos]
        msg = '{.__name__!r} object has no attribute {!r}'
        raise AttributeError(msg.format(cls, name))

    def __setattr__(self, name, value):
        """
        객체의 속성을 설정할 때 호출함. 속성 할당 연산이 발생할 때마다 호출됨. 
        이를 통해 속성 설정 동작을 커스터마이징할 수 있음
        
        # 용도
        - 속성 설정 로깅 : 속성 설정 시 로그를 남길 수 있음
        - 속성 값 검증 : 속성 값의 유효성을 검증할 수 있음
        - 속성 값 변환 : 설정된 값을 변환하거나 가공가능 
        """
        cls = type(self)
        if len(name) == 1:  # <1>
            if name in cls.shortcut_names:  # <2>
                error = 'readonly attribute {attr_name!r}'
            elif name.islower():  # <3>
                error = "can't set attributes 'a' to 'z' in {cls_name!r}"
            else:
                error = ''  # <4>
            if error:  # <5>
                msg = error.format(cls_name=cls.__name__, attr_name=name)
                raise AttributeError(msg)
        super().__setattr__(name, value)  # <6>
    
    def angle(self, n):  # <2>
        """특정 좌표의 각 좌표를 계산"""
        r = math.sqrt(sum(x * x for x in self[n:]))
        a = math.atan2(r, self[n-1])
        if (n == len(self) - 1) and (self[-1] < 0):
            return math.pi * 2 - a
        else:
            return a
        

    def angles(self):  # <3>
        """모든 각 좌표의 반복형을 반환함"""
        return (self.angle(n) for n in range(1, len(self)))

    def __format__(self, fmt_spec=''):
        """
        객체가 특정 형식으로 문자열로 변환될 때 호출됨. 해당 메서드는 format() 함수나 문자열의 format() 메서드에 
        의해 사용됨
        
        # 용도
        - 사용자 정의 형식 지정 
        - 형식 코드 지원 : 객체의 문자열 표현을 세부적으로 조정할 수 있음 
        """
        if fmt_spec.endswith('h'):  # hyperspherical coordinates
            fmt_spec = fmt_spec[:-1]
            coords = itertools.chain([abs(self)],
                                     self.angles())  # <4>
            outer_fmt = '<{}>'  # <5>
        else:
            coords = self
            outer_fmt = '({})'  # <6>
            
        components = (format(c, fmt_spec) for c in coords)  # <7>
        return outer_fmt.format(', '.join(components))  # <8>

    @classmethod
    def frombytes(cls, octets):
        """
        @classmethod는 클래스 메서드 정의할 때 사용하는 데코레이터
        
        # 특징 
        - 클래스 메서드에는 cls로 클래스 자체를 첫 번째 인자로 받음 
        - 스태틱 변수(cv) 사용하면서 작업 처리
        - 인스턴스가 아닌 클래스 자체에 바인딩 
        """
        typecode = chr(octets[0])
        memv = memoryview(octets[1:]).cast(typecode)
        return cls(memv)
```

### 11. 파이썬에서 일반적인 매핑형

<img src="https://github.com/user-attachments/assets/9601b35f-e9ff-40f7-9680-8e692eee2353" width="500" height="500"/>

- ABC : Abstract Base Class, 추상 베이스 클래스
- collections.abc 는 자바로 따지면 Collection 프레임워크임
- 위의 사진에서 알 수 있는 것, 각각 가장 기본 단위의 인터페이스를 만듦. 이를 조합해서 하나의 큰 인터페이스를 만듦. 또 이를 구현해나가면서 특정 클래스를 구현함
- Container, Iterable, Sized, Mapping 모두 불변/ MutableMapping에서는 앞의 불변 인터페이스를 모두 상속 받고 추가적으로 변경 메서드를 추가해서 가변으로 재정의함


### 12. "해시 가능하다"의 의미?

해시란? 디지털 지문, 각 객체마다 고유의 지문이 있는 느낌

<br>

자바에서 해시 가능하다의 의미는 2가지 의미를 나타냄
- (1) 여러번 호출해도 같은 값
- (2) 해시값이 같으면 equals() 가 True

<br>

- 가변 객체는 해시 불가능한 객체임. 즉, 해시 가능한 객체는 불변
- 불변 내장 객체에서 가변 객체를 참조하면 해시 불가능함

### 13. memoryview : 메모리를 어떻게 활용할 건가

- 배열은 기본적으로 1 byte가 기본임
  - int 배열의 경우 기본 단위가 4 byte
- 즉, 모든 배열은 byte 배열이고 이것을 어떤 단위로 쪼개서 사용할 것인가를 의미함 

### 📋 몰입 리스트

