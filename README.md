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


명확한 코드는 암시적인 코드보다 낫다.
단순한 코드가 복잡한 코드보다 낫다.
복잡한 코드가 난해한 코드보다 낫다.
단조로운 코드가 복잡한 코드보다 낫다.
읽기 쉬운 코드는 읽기 어려운 코드보다 낫다.
가독성은 중요하다.
규칙을 깰 정도로 특별한 경우란 없다.
하지만 실용성은 이상을 능가한다.
에러를 결코 조용히 넘어가지 않도록 한다.
명시적으로 조용히 넘어가라고 하더라도 조용히 넘어가지 않는다.
모호한 코드를 대면할 때마다 추측하고 싶은 유혹을 거절하라.
문제를 해결할 단 하나의 명확하고 바람직한 방법이 있을 것이다.
하지만 처음에 코딩을 할 때는 잘 모를 수 있기에 코드의 동작 방법을 정확히 알지 못할 수 있다.
아무것도 안 하는 것보다 지금 하는 게 낫다.
하지만 아무것도 하지 않는 것이 지금 당장 하는 것보다 나을 수도 있다.
설명하기 어려운 구현이라면 좋은 아이디어는 아니다.
쉽게 설명할 수 있는 구현이라면 좋은 아이디어일 것이다.
네임스페이스는 매우 훌륭한 아이디어이다. 많이 사용하자

```

<br>

# 01. 들어가며
(참고 해볼만한 사이트 : http://www.pythontutor.com/)


## 📌 01. 파이썬 데이터 모델 

#### 👉 파이썬 데이터 모델

> - 파이썬의 최고의 장점은 '일관성'. 이를 통해 새로운 기능에 대해서도 제대로 예측 가능함
> - 데이터 모델은 일종의 프레임워크로서, 파이썬을 설명하는 것이라고 생각할 수 있음
> - 시퀀스, 반복자, 함수, 클래스, 콘텍스트 관리자 등 언어 자체의 구성단위에 대한 인터페이스를 공식적으로 정의함
> - 파이썬 인터프리터는 특별 메서드를 호출해서 기본적인 객체 연산을 수행하는데, 종종 특별한 구문에 의해 호출됨
>   - 예를 들어서, obj[key] 형태의 구문은 `__getitem__()` 특별 메서드가 지원함.
>   - my_collection[key]를 평가하기 위해 인터프리터는 my_collection.`__getitem__(key)`를 호출함
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
> - FrenchDeck 클래스는 간단하지만 많은 기능을 구현함. 파이썬의 특징과 특별 메서드를 통해 파이썬 데이터 모델을 사용할 때의 이점을 파악
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

#### 특별 메서드명(연산자 제외)

| 범주               | 메서드명                                                                 |
|--------------------|--------------------------------------------------------------------------|
| 문자열/바이트 표현 | `__repr__`, `__str__`, `__format__`, `__bytes__`                         |
| 숫자로 변환        | `__abs__`, `__bool__`, `__complex__`, `__int__`, `__float__`, `__hash__`, `__index__` |
| 컬렉션 에뮬레이션  | `__len__`, `__getitem__`, `__setitem__`, `__delitem__`, `__contains__`   |
| 반복               | `__iter__`, `__reversed__`, `__next__`                                  |
| 콜러블 에뮬레이션  | `__call__`                                                              |
| 콘텍스트 관리      | `__enter__`, `__exit__`                                                 |
| 객체 생성 및 소멸   | `__new__`, `__init__`, `__del__`                                       |
| 속성 관리          | `__getattr__`, `__getattribute__`, `__setattr__`, `__delattr__`, `__dir__` |
| 속성 디스크립터    | `__get__`, `__set__`, `__delete__`                                      |
| 클래스 서비스      | `__prepare__`, `__instancecheck__`, `__subclasscheck__`                 |

---

#### 연산자에 대한 특별 메서드명

| 범주                  | 메서드명 및 관련 연산자                                                                |
|-----------------------|---------------------------------------------------------------------------------------|
| 단항 수치 연산자      | `__neg__ -`, `__pos__ +`, `__abs__` (abs())                                           |
| 항등된 비교 연산자    | `__lt__ <`, `__le__ <=`, `__eq__ ==`, `__ne__ !=`, `__gt__ >`, `__ge__ >=`            |
| 산술 연산자           | `__add__ +`, `__sub__ -`, `__mul__ *`, `__truediv__ /`, `__floordiv__ //`, `__mod__ %`, `__divmod__` (divmod()), `__pow__ **` (pow()), `__round__` (round()) |
| 역순 산술 연산자      | `__radd__`, `__rsub__`, `__rmul__`, `__rtruediv__`, `__rfloordiv__`, `__rmod__`, `__rdivmod__`, `__rpow__` |
| 복합 할당 산술 연산자 | `__iadd__`, `__isub__`, `__imul__`, `__itruediv__`, `__ifloordiv__`, `__imod__`, `__ipow__` |
| 비트 연산자           | `__invert__ ~`, `__lshift__ <<`, `__rshift__ >>`, `__and__ &`, `__or__\|` , `__xor__ ^` |
| 역순 비트 연산자      | `__rlshift__`, `__rrshift__`, `__rand__`, `__rxor__`, `__ror__`                       |
| 복합 할당 비트 연산자 | `__ilshift__`, `__irshift__`, `__iand__`, `__ixor__`, `__ior__`                       |

<br>

#### 👉 왜 len()은 메서드가 아닐까?

> - '파이썬 선'에서 <strong>실용성이 순수성에 우선한다.</strong>라는 말이 있음
> - len(x)는 x가 내장형의 객체일 때 빨리 실행됨. CPython의 내장 객체에 대해서는 메서드를 호출하지 않고 단지 C언어 구조체의 필드를 읽어올 뿐임
> - 컬렉션에 들어 있는 항목 수를 가져오는 연산은 자주 발생하기에 str, list, memoryview 등의 다양한 기본형 객체에 대해 효율적으로 작동해야함
> - 즉, len()은 abs()와 마찬가지로 파이썬 데이터 모델에서 특별한 대우를 받으므로 메서드라고 부르지 않음
> - 물론 `__len__()` 특별 메서드 덕분에 내가 정의한 객체에서 len() 메서드를 직접 정의할 수 있음

<br>

#### 👉 요약 

> - <strong>특별 메서드를 구현하면 사용자 정의 객체도 내장형 객체처럼 작동하게 되어 '파이썬스러운' 표현력 있는 코딩 스타일을 구사할 수 있음</strong>
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

<br>
<br>


# 02. 데이터 구조체 


## 📌 01. 시퀀스   

<br>

#### 👉 시퀀스란?

> - 파이썬은 시퀀스를 단일하게 처리하는 ABC의 특징을 물려받음. 문자열, 리스트, 바이트 시퀀스, 배열 ... 모두 반복, 슬라이싱, 정렬, 연결 등 공통된 연산을 적용할 수 있음
> - <strong>파이썬에서 제공하는 다양한 시퀀스를 이해하면 코드를 새로 구현할 필요가 없으며, 시퀀스의 공통 인터페이스를 따라 기존 혹은 향후에 구현될 시퀀스 자료형을 적절히 지원하고 활용할 수 있게 API를 정의할 수 있음</strong>

<br>

#### 👉 내장 시퀀스 개요

> - <img src="https://github.com/user-attachments/assets/a10871a5-cb84-474a-8838-3489818da38a" width="500" height="500"/>
> - 파이썬 표준 라이브러리는 C로 구현된 더음과 같은 시퀀스 형 제공
>   - <strong> 1. 컨테이너 시퀀스 : 서로 다른 자료형의 항목을 담을 수 있는 list, tuple, collections, deque ...</strong>
>   - <strong> 2. 균일 시퀀스 : 단 하나의 자료형만 담을 수 있는 str, bytes, bytearray, memoryview, ...</strong>
>   - 컨테이너 시퀀스는 객체에 대한 참조를 담고 있으며 객체는 어떠한 자료형도 될 수 있지만, 균일 시퀀스는 객체에 대한 참조 대신 자신의 메모리 공간에 각 항목의 값을 직접 담음
> - 가변성에 따라 분류할 수 있음
>   - <strong> 1. 가변 시퀀스 : 변경 가능한 시퀀스 list, bytes, array.array, collections.deque, memoryview, ... </strong>
>   - <strong> 2. 불변 시퀀스 : 변경 불가능한 시퀀스 tuple, str, bytes, ... </strong>

<br>

#### 👉 지능형 리스트와 제너레이터 표현식 

```python

# 지능형 리스트 잘 활용한 사례
symbols = '$%!@#$'
codes = [ord(symbol) for symbol in sybols]

# 지능형 리스트는 함수처럼 고유한 지역 범위를 갖음
x = 'ABC'
dummy = [ord(x) for x in x]
x # 'ABC'
dummy # [65, 66, 67]

# 지능형 리스트와 맵/필터 구성으로 만든 동일 리스트
symbols = '$%!@#$'
beyond_ascii = [ord(s) for s in symbols if ord(s) > 127]
beyond_ascii


beyond_ascii = list(filter(lambda c: c > 127, map(ord, symbols)))
beyond_ascii

# 제너레이터 표현식에서 튜플과 배열 초기화하기
symbols = '$%!@#$'
tuple(ord(s) for s in symbols)

import array
array.array('I', (ord(s) for s in symbols)) # 배열 생성자의 첫 번째 인수는 배열에 들어 갈 숫자들을 저장할 자료형을 지정

```

> - <strong>지능형 리스트(리스트형의 경우)나 제너레이터 표현식(그 외 시퀀스의 경우)을 사용하면 시퀀스를 간단하면서도 가독성 좋게 생성할 수 있음</strong>
> - 위의 코드를 보면 알수 있듯이 잘 짜여진 지능형 리스트는 그 의도가 명확하고 깔끔함. 물론 지능형 리스트를 막 쓰면 되려 가독성이 떨어질 수 있음
> - 지능형 리스트, 제너레이터 표현식, 그리고 이와 동급인 지능형 집합과 지능형 딕셔너리는 함수처럼 고유한 지역 범위(스코프)를 갖음
> - 표현식 안에서 할당된 변수는 지역 변수지만, 주변 범위의 변수를 여전히 참조할 수 있음
> - map()과 filter()를 이용해서 수행할 수 있는 작업은 기능적으로 문제가 있는 파이썬 람다를 억지로 끼워 넣지 않고도 지능형 리스트를 이용해서 모두 구현가능함
> - 튜플, 배열 등의 시퀀스형을 초기화하려면 지능형 리스트를 사용할 수도 있지만, <strong>다른 생성자에 전달할 리스트를 통째로 만들지 않고 반복자 프로토콜을 이용해서 항목을 하나씩 생성하는 제너레이터 표현식은 메모리를 더 적게 사용함</strong>
> - 리스트 이외의 시퀀스를 초기화하거나, 메모리에 유지할 필요가 없는 데이터를 생성하기 위해 제너레이터 표현식을 사용함


<br>

#### 👉 튜플은 단순한 불변 리스트가 아니다

> - 튜플은 불변 리스트로 사용할 수도 있지만, 필드명이 없는 레코드로 사용할 수도 있음


<br>

#### 👉 레코드로서의 튜플 

```python
lax_coordinates = (33.9425, -188.408056)
city, year, pop, chg, area = ('Tokyo', 2003, 32450, 0.66, 8014)
traveler_ids = [('USA', '31195855'), ('BRA', 'CE342567'), ('ESP', 'XDA205856')]

for passport in sorted(traveler_ids) :
  print('%s%s' % passport)

# >> BRA/CE342567
# >> ESP/XDA205856
# >> USA/31195855


for country, _ in traveler_ids :
  print(country)

# >> USA
# >> BRA
# >> ESP
```

> - 튜플은 레코드를 담고 있음. 튜플의 각 항목은 레코드의 필드 하나를 의미하여 항목의 위치가 의미를 결정함
> - 튜플을 필드의 집합으로 사용하는 경우에는 항목 수가 고정되어 있고 항목의 순서가 중요함
> - 튜플 안에서 항목의 위치가 항목의 의미를 나타내므로 튜플을 정렬하면 정보가 파괴된다는 점에 주의해야함
> - 튜플은 언패킹 매커니즘 덕분에 레코드로도 잘 동작함

<br>

#### 👉 튜플 언패킹 


```python
# 튜플 언패킹 대표 사례 
lax_coordinates = (33.9425, -188.408056)
city, year, pop, chg, area = ('Tokyo', 2003, 32450, 0.66, 8014) # 언패킹 활용 - 병렬 할당(반복형 데이터를 변수로 구성된 튜플에 할당하는 것을 말함)
traveler_ids = [('USA', '31195855'), ('BRA', 'CE342567'), ('ESP', 'XDA205856')]

for passport in sorted(traveler_ids) :
  print('%s%s' % passport) # 언패킹 활용

# >> BRA/CE342567
# >> ESP/XDA205856
# >> USA/31195855


for country, _ in traveler_ids :
  print(country)

# >> USA
# >> BRA
# >> ESP

# 튜플 언팩킹 활용

b, a = a, b # 스왑

t = (20, 9)
quotient, remainder = divmod(*t)
quotient, remainder
# >> (2, 4)

# 함수에서 호출자에 여러 값을 간단히 반환하는 기능
import os
_, filename = os.path.split('/home/luciano/.ssh/idrsa.pub')
filename

# >> 'idrsa.pub'

# 초과 항목을 잡기 위해 * 사용하기
a, b, *res = range(5)
a, b, rest
# >> (0, 1, [2, 3, 4])

```


> - 위의 예시를 보면 city, year, pop, chg, area 변수에 ('Tokyo' 2003, 32450, 0.66, 8014)를 할당함
> - 또한, 퍼센트(%) 연산자는 print() 함수의 인수로 전달한 포맷 문자열의 각 슬롯에 passport 튜플의 각 항목을 할당함
> - 위 두가지 부분이 '튜플 언패킹' 방법을 보여줌
> - 튜플 언패킹은 반복 가능한 객체라면 어느 객체든 적용할 수 있음
> - 튜플에는 '병렬 할당'이 있음. 이는 반복형 데이터를 변수로 구성된 튜플에 할당하는 것을 말함
> - 함수 매개변수에 *를 연결해서 초과된 인수를 가져오는 방법은 파이썬의 고전적인 기능임. 이를 확장해서 병렬 할당처리 가능함


<br>

#### 👉 내포된 튜플 언팩킹 

```python
metro_areas = [
  ('Tokyo', 'JP', 36.933, (35.689722, 139.691667)),
  ('Delhi NCR', 'IN', 21.935, (28.613889, 77.208889)),
  ... 
]

print('{:15} | {:^9} | {:^9}'.format('', 'lat.', 'long.'))
fmt = '{:15} | {:9.4f} | {:9.4f}'

for name, cc, pop, (latitude, longitude) in metro_areas :
  if logitude <= 0 :
    print(fmt.format(name, latitude, longitude))


# >>             |  lat.    |   long.   |
# >> Mexico City |  19.4333 |  -99.1333 |
# >>            ... 
```

> - 언패킹할 표현식을 받는 튜플은 (a, b, (c, d)) 처럼 다른 튜플을 내포할수 있음



<br>


#### 👉 명명된 튜플

```python
# 명명된 튜플형을 정의하고 사용하기
from collections import namedtuple

City = namedtuple('City', 'name country population coordinates')
tokyo = City('Tokyo', 'JP', 36.933, (35.689722, 139.691667))
tokyo

# >> City(name='Tokyo'm country='JP', population=36.933, coordinates=(35.689722, 139.691667))


```

> - collections.namedtuple()은 필드명(iv)과 클래스명을 추가한 튜플의 서브 클래스를 생성하는 팩토리 함수
> - 이는 디버깅할 때나 간단한 클래스를 구현할 때 매유 유용함
> - 필드명이 클래스에 저장되므로 namedtuple()로 생성한 객체는 튜플과 동일한 크기의 메모리만 사용함
> - 속성을 객체마다 존재하는 `__dict__` 에 저장하지 않으므로 일반적인 객체보다 메모리를 적게 사용함


<br>


#### 👉 불변 리스트로서의 튜플

| 메서드               | 리스트 | 튜플 | 설명                                                               |
|----------------------|--------|------|--------------------------------------------------------------------|
| `s.__add__(s2)`      | ●      | ●    | `s + s2` — 리스트를 연결한다.                                      |
| `s.__iadd__(s2)`     | ●      |      | `s += s2` — 리스트를 연결하고 s에 저장한다.                        |
| `s.append(e)`        | ●      |      | 제일 뒤에 요소를 하나 추가한다.                                    |
| `s.clear()`          | ●      |      | 모든 항목을 삭제한다.                                              |
| `s.__contains__(e)`  | ●      | ●    | `e in s`                                                          |
| `s.copy()`           | ●      |      | 리스트를 얕게 복사한다.                                            |
| `s.count(e)`         | ●      | ●    | `e`가 발생한 횟수를 계산한다.                                      |
| `s.__delitem__(p)`   | ●      |      | `p` 위치의 요소를 삭제한다.                                       |
| `s.extend(it)`       | ●      |      | 반복형 `it` 안에 있는 요소를 추가한다.                             |
| `s.__getitem__(p)`   | ●      | ●    | `s[p]` — `p` 위치의 요소를 가져온다.                               |
| `s.__getnewargs__()` | ●      | ●    | `pickle`을 이용해서 최적화된 직렬화를 지원한다.                    |
| `s.index(e)`         | ●      | ●    | `s` 안에서 `e`가 처음 나타나는 위치를 찾는다.                      |
| `s.insert(p, e)`     | ●      |      | `p` 위치에 있는 요소 앞에 `e` 요소를 삽입한다.                     |
| `s.__iter__()`       | ●      | ●    | 반복자를 가져온다.                                                 |
| `s.__len__()`        | ●      | ●    | `len(s)` — 항목 개수를 구한다.                                     |
| `s.__mul__(n)`       | ●      | ●    | `s * n` — 문자열을 반복한다.                                       |
| `s.__imul__(n)`      | ●      |      | `s *= n` — 문자열을 반복하여 `s`에 저장한다.                       |
| `s.__rmul__(n)`      | ●      | ●    | `n * s` — 역순 반복기 메서드(역순 연산자는 13장에서 설명한다).      |
| `s.pop([p])`         | ●      |      | 마지막 항목이나 `p` 위치의 항목을 제거하고 반환한다.               |
| `s.remove(e)`        | ●      |      | `e` 값을 가진 첫 번째 항목을 삭제한다.                             |
| `s.reverse()`        | ●      |      | 항목을 역순으로 배치한 후 `s`에 저장한다.                          |
| `s.__reversed__()`   | ●      |      | 마지막에서 첫 번째 항목까지 반복하는 반복자를 반환한다.            |
| `s.__setitem__(p, e)`| ●      |      | `s[p] = e` — `p` 위치에 저장하는 기존 항목을 `e`로 설정한다.      |
| `s.sort([key], [reverse])` | ● | | 선택적인 키워드 `key`와 `reverse`에 따라 항목을 정렬하고 `s`에 저장한다. |


> - 튜플을 불변 리스트로 사용할 때, 튜풀과 리스트가 얼마나 비슷한지 알고 있으면 도움이 됨


<br>


#### 👉 슬라이싱 

> - 파이썬에서 제공하는 list, tuple, str, 그리고 모든 시퀀스형은 슬라이싱 연산을 지원함
> - 슬라이싱 연산은 강력한 기능임

<br>


#### 👉 슬라이스와 범위 지정시에 마지막 항목이 포함되지 않는 이유


```python

l = [10, 20, 30, 40, 50, 60]
l[:2]

# > [10, 20]

l[2:]

# > [30, 40, 50, 60]

l[:3]

# > [10, 20, 30]

l[3:]

# > [40, 50, 60]

```

> - 슬라이스와 범위 지정시에 마지막 항목을 포함하지 않는 관례는 인덱스 번호가 0부터 시작하는 파이썬, C 등의 언어에서 잘 작동함
> - 이 관례 덕분에 아래와 같은 장점이 있음
>   - (1) 세 개의 항목을 생성하는 range(3)나 my_list`[:3]` 처럼 중단점만 이용해서 슬라이스나 범위를 지정할 때 길이를 계산하기 쉬움
>   - (2) 시작점과 중단점을 모두 지정할 때도 길이를 계산하기 쉬움. 단지 중단점에서 시작점을 빼면됨
>   - (3) 위의 예제처럼 x 인덱스를 기준으로 겹침없이 시퀀스를 분할하기 쉬움. 단지 my_list`[:x]`와 my_list`[x:]`로 지정하면 됨   

<br>


#### 👉 슬라이스 객체 


```python

s = 'bicyle'
s[::3]

# > 'bye'

s[::-1]

# > 'elcycib' 

```

> - s`[a:b:c]`는 c 보폭만큼 항목씩 건너뜀. 보폭이 음수인 경우에는 거꾸로 거슬러 올라가 항목을 반환함
> - a:b:c 표기법은 인덱스 연산을 수행하는 `[]` 안에서만 사용할 수 있으ㅁ, slice(a, b, c) 객체를 생성함
> - 파이썬은 seq`[start:stop:step]` 표현식을 평가하기 위해 seq.`__getitem__(slice(start, stop, step))`을 호출함

<br>

#### 👉 다차원 슬라이싱과 생략 기호 


> - `[]` 연산자는 콤마로 구분해서 여러 개의 인덱스나 슬라이스를 가질 수 있음
> - 이 방법은 NumPy 외부 패키지에서 a[i, j] 구문으로 2차원 numpy.ndarray 배열의 항목이나 a[m:n. k:l] 구문으로 2차원 슬라이스를 가져올 때 사용함
> - `[]` 연산자를 처리하는 `__getitem__()`과 `__setitem__()` 특수 메서드는 a[i, j]에 들어 있는 인덱스들을 튜플로 받음
> - 즉, a[i, j]를 평가하기 위해 파이썬은 a.`__getitem__((i, j)`를 호출함
> - 슬라이스는 시퀀스에서 정보를 추출할 뿐만 아니라 가변 시퀀스의 값을 변경할 때도(즉, 시퀀스를 새로 만드는 것이 아니라 일부 항목의 값을 시퀀스 안에서 직접 변경함) 사용할 수 있음

<br>

#### 👉 슬라이스에 할당하기 


```python

l = list(range(10))
l

# > [0, 1, 2, ..., 9]

l[2:5] = [20, 30]
l

# > [0, 1, 20, 30, 5, 6, 7, 8, 9]

del l[5:7]
l

# > [0, 1, 20, 30, 5, 8, 9]

```

> - 할당문의 왼쪽에 슬라이스 표기법을 사용하거나 del 문의 대상 객체로 지정함으로써 가변 시퀀스를 연결하거나, 잘라 내거나, 값을 변경할 수 있음
> - 할당문의 대상이 슬라이스인 경우, 항목 하나만 할당하는 경우에도 할당문 오른쪽에는 반복 가능한 객체가 와야함


<br>

#### 👉 시퀀스에 덧셈과 곱셈 연산자 사용하기  


```python

l = [1, 2, 3]
l * 3

# > [1, 2, 3, 1, 2, 3, 1, 2, 3]

3 * 'abc'

# > 'abcabcabc'

# 리스트의 리스트 만들기

## (1) 정상적인 경우
board = [['_'] * 3 for i in range(3)]
board

# > [['_', '_', '_'], ['_', '_', '_'], ['_', '_', '_']]

board[1][2] = 'X'
board

# > [['_', '_', '_'], ['_', '_', 'X'], ['_', '_', '_']]


## (2) 비정상적인 경우(쓸모 없는 경우)
board = [['_'] * 3] * 3 # 최상위 리스트가 동일한 내부 리스트에 대한 참조 세 개를 가짐 
board

# > [['_', '_', '_'], ['_', '_', '_'], ['_', '_', '_']]

board[1][2] = 'X'
board

# > [['_', '_', 'X'], ['_', '_', 'X'], ['_', '_', 'X']]

```

> - 시퀀스에서는 덧셈(+)와 곱셈(*)을 지원함
>   - (1) 덧셈의 경우 피연산자 두 개가 같은 자료형이어야 하며, 둘 다 변경되지 않지만 동일한 자료형의 시퀀스가 새로 만들어짐
>   - (2) 곱셈의 경우 하나의 시퀀스를 여러 번 연결할 때 사용하며 이때에도 새로운 시퀀스가 만들어짐
> - 덧셈 및 곱셈 연산자는 언제나 객체를 새로 만들고, 피연산자를 변경하지 않음
> - a가 가변 항목을 담고 있을 때 a * n 과 같은 표현식을 사용하려면 주의해야함. 원치 않는 결과가 발생할 수 있음
>   - my_list = `[[]]` * 3 으로 초기화하면 동일한 내부 리스트에 대한 참조 세 개를 가진 리스트가 만들어짐


<br>

#### 👉 시퀀스의 복합 할당 

```python

# += 연산자 작동하는 방식 탐구
a += b

# *= 연산자를 가변 시퀀스와 불변 시퀀스에 적용한 예
l = [1, 2, 3] # 현재 가변 시퀀스(in-place) 
id(l) # id() : 해시코드 : 객체 지문(디지털 지문) 

# > 345246147

l *= 2 # 내부적으로 __iadd__()를 호출함
l

# > [1, 2, 3, 1, 2, 3]

id(l)
# > 345246147

t = (1, 2, 3)
id(t)
# > 876765543

t *= 2
id(t)
# > 237492031

# list : 가변 - 연산수행(변경) - 같은 객체 반환
# tuple : 불변 - 연산수행(변경) - 새로운 객체 생성 

```

> - *= 연산자가 작동하도록 만드는 특수 메서드는 `__iadd__()`임
> - 그런데, `__iadd__()` 메서드가 구현되어 있지 않으면, 파이썬은 대신 `__add__()` 메서드를 호출함.
> - 예를 들어서, a += b가 있다고 가정했을 때
> - a가 `__iadd__()` 메서드를 구현하면 구현된 메서드가 호출됨. a가 list, bytearray, array.array 등 가변 시퀀스인 경우 a의 값이 변경됨(이 과정은 a.extend(b)와 유사함)
> - 그런데 a가 `__iadd__()` 메서드를 구현하지 않는 경우 a += b 표현식은 a = a + b가 되어 먼저 a + b 를 평가하고, 객체를 새로 생성한 후 a에 할당함
> - 즉, `__iadd__()` 메서드 구현 여부에 따라 a 변수가 가리키는 객체의 정체성이 바뀔 수도 있고 바뀌지 않을 수도 있음
> - 일반적으로 가변 시퀀스에 대해 `__iadd__()` 메서드를 구현해서 += 연산자가 기존 객체의 내용을 변경하게 만드는 것이 좋음. 불변 시퀀스의 경우에는 이 연산을 수행할 수 없음
> - 가변 항목을 튜플에 넣는 것은 좋은 생각이 아님
> - 복합 할당은 원자적인 연산이 아님
> - 파이썬 바이트코드르 살펴보는 것은 그리 어렵지 않으며, 내부에서 어떤 일이 발생하고 있는지 살펴보는 데 도움이 됨


<br>

#### 👉 list.sort()와 sorted() 내장 함수

```python

fruits = ['grape', 'raspberry', 'apple', 'banana']

sorted(fruits)
# > ['apple', 'banana', 'grape', 'raspberry']

fruits
# > ['grape', 'raspberry', 'apple', 'banana']

sorted(fruits, reverse=True)
# > ['raspberry', 'grape', 'banana', 'apple']

fruits.sort()
fruits
# > ['apple', 'banana', 'grape', 'raspberry']

```

> - list.sort() 메서드는 사본을 만들지 않고 리스트 내부를 변경해서 정렬함. sort() 메서드는 타깃 객체를 변경하고 새로운 리스트를 생성하지 않았음을 알려주기 위해 None을 반환함
> - random.shuffle() 함수도 이와 동일하게 작동함
> - 이와 반대로 sorted() 내장 함수는 새로운 리스트를 생성해서 반환함
> - 사실 sorted() 함수는 불변 시퀀스 및 제너레이터를 포함해서 반복 가능한 모든 객체를 인수로 받을 수 있음
> - 입력받은 반복 가능한 객체의 자료형과 무관하게 sorted() 함수는 언제나 새로 생성한 리스트를 반환함
> - list.sort()와 sorted() 함수 모두 선택적으로 두 개의 키워드를 인수로 받음
>   - (1) reverse : 이 키워드가 참이면 비교 연산을 반대로 해서  내림차순으로 반환함. 기본값은 False
>   - (2) key : 정렬에 사용할 키를 생성하기 위해 각 항목에 적용할 함수를 인수로 받음. 예를 들어 문자열의 리스트를 정렬할 때 key=str.lower로 지정하면 대소문자를 구분하지 않고 정렬함


<br>

#### 👉 정렬된 시퀀스를 bisect로 관리하기 

```python
import bisect
import sys

HAYSTACK = [1, 4, 5, 6, 8, 12, 15, 20, 21, 23, 23, 26, 29, 30]
NEEDLES = [0, 1, 2, 5, 8, 10, 22, 23, 29, 30, 31]

ROW_FNT = '{0:2d} @ {1:2d}    {2}{0:<2d}'

def demo(bisect_fn) :
  for needle in reversed(NEEDLES) :
      position = bisect_fn(HAYSTACK, needle)
      offset = position * '  |'
      print(ROW_FNT.format(needle, position, offset))

if __name__ == '__main__' :
  if sys.argv[-1] == 'left' :
    bisect_fn = bisect.bisect_left

  else :
    bisect_fn = bisect.bisect

print('DEMO : ', bisect_fn.__name__)
print('haystack ->', ' '.join('%2d' % n for n in HAYSTACK))
demo(bisect_fn)

# 실행 결과 나중에 추가하기  


```

> - bisect 모듈은 bisect()와 insort() 함수를 제공함. bisect()는 이진 검색 알고리즘을 이용해서 시퀀스를 검색하고, insort()는 정렬된 시퀀스 안에 항목을 삽임함
> - bisect(haystack, needle)은 정렬된 시퀀스인 haystack 안에서 오름차순 정렬 상태를 유지한 채로 needle을 추가할 수 있는 위치를 찾아냄. 즉, 해당 위치 앞에는 needle보다 같거나 작은 항목이 옴
> - bisect(heystack, needle)의 결과값을 인덱스(index)로 사용해서 haystack.insert(index, needle)을 호출하면 needle을 추가할 수 있지만, insort()는 이 두 과정을 더 빠르게 처리함
> - bisect의 행동은 두 가지 방식으로 조절 가능함
>   - (1) 선택 인수 lo와 hi를 사용하면 삽입할 때 검색할 시퀀스 영역을 좁힐 수 있음. lo의 기본값은 0, hi의 기본값은 시퀀스의 len()
>   - (2) bisect는 실제로 bisect_right() 함수의 별명이며, 이 함수의 자매 함수로 bisect_left()가 있음.
>   - bisect_right()는 기존 항목 바로 뒤를 삽입 위치로 반환하며, bisect_left()는 기존 항목 위치를 삽입 위치로 반환하므로 기존 항목 바로 앞에 삽입됨



<br>

#### 👉 bisect.insort()로 삽입하기

```python

import bisect
import random

SIZE = 7
random.seed(1729)

my_list = []
for i in range(SIZE) :
  new_item = random.randrange(SIZE*2)
  bisect.insort(my_list, new_item)
  print('%2d -> ' % new_item, my_list)

```

> - 정렬은 값비싼 연산임(nlogn이 가장 빠른 정렬 알고리즘임)
> - 따라서, 시퀀스를 정렬한 후에는 정렬 상태를 유지하는 것이 좋음. 그렇기에 bisect.insort() 함수가 만들어짐
> - insort(seq, item)은 seq를 오름차순으로 유지한 채로 item을 seq에 삽입함
> - bisect 함수와 마찬가지로 insort 함수도 선택적으로 lo와 hi 인수를 받아 시퀀스 안에서 검색할 범위를 제한함
> - 그리고 삽입 위치를 검색하기 위해 bisect_left() 함수를 사용하는 insort_left() 함수도 있음
> - 지금까지 설명한 내용은 리스트, 튜플, 시퀀스에 적용됨


<br>

#### 👉 리스트가 답이 아닐 때


> - 리스트형은 융통성이 있고 사용하기 편함. 하지만, 항상 리스트를 사용하는 것이 효율적인 것은 아님
>   - (1) 배열 -> 실수를 천만 개 저장해야 하는 경우, 파이썬의 배열은 C언어의 배열과 마찬가지로 기계가 사용하는 형태로 표현된 바이트 값만 저장하기에 더 효율적임
>   - (2) 덱(deque) -> LIFO, FIFO 데이터 구조를 구현할 때 덱(deque)가 더 효율적임
> - 밑에 자세한 설명을 통해 리스트를 대체할 수 있는 여러 시퀀스를 살펴보자

<br>

#### 👉 배열

| 메서드                  | 리스트 | 배열 | 설명                                                                          |
|-----------------------|--------|------|------------------------------------------------------------------------------|
| `s.__add__(s2)`      | •      |      | `s + s2` — 연결합니다.                                                        |
| `s.__iadd__(s2)`     | •      |      | `s += s2` — 연결하고 `s`에 할당합니다.                                        |
| `s.append(e)`        | •      |      | `e`를 리스트의 끝에 추가합니다.                                               |
| `s.byteswap()`       |        | •    | 모든 요소의 바이트 순서를 변경하여 엔디안을 변환합니다.                        |
| `s.clear()`          | •      |      | 모든 항목을 제거합니다.                                                       |
| `s.__contains__(e)`  | •      |      | `e in s` — 포함 여부를 확인합니다.                                            |
| `s.copy()`           | •      |      | 리스트의 얕은 복사본을 반환합니다.                                            |
| `s.__copy__()`       | •      |      | `copy.copy()` 메서드를 지원합니다.                                            |
| `s.count(e)`         | •      |      | `s`에서 `e`의 발생 횟수를 반환합니다.                                         |
| `s.__deepcopy__()`   | •      |      | `copy.deepcopy()`을 지원합니다.                                               |
| `s.__delitem__(p)`   | •      |      | 위치 `p`에 있는 항목을 삭제합니다.                                            |
| `s.extend(it)`       | •      |      | 반복 가능한 객체 `it`의 요소들을 추가하여 리스트를 확장합니다.                 |
| `s.frombytes(b)`     |        | •    | 바이트 시퀀스에서 기계 값을 해석하여 항목을 추가합니다.                       |
| `s.fromfile(f, n)`   |        | •    | 열린 파일 `f`에서 `n`개의 항목을 기계 값으로 해석하여 추가합니다.              |
| `s.fromlist(l)`      |        | •    | 리스트 `l`에서 항목을 추가합니다. 한 번 이상 호출하면 `TypeError`가 발생합니다. |
| `s.__getitem__(p)`   | •      |      | 위치 `p`에 있는 항목을 반환합니다.                                            |
| `s.index(e)`         | •      |      | `e`의 인덱스를 반환합니다.                                                    |
| `s.insert(p, e)`     | •      |      | 위치 `p`에 `e`를 삽입합니다.                                                  |
| `s.itemsize`         |        | •    | 각 항목의 바이트 크기를 반환합니다.                                           |
| `s.__iter__()`       | •      |      | 반복자를 반환합니다.                                                          |
| `s.__len__()`        | •      |      | `len(s)` — 항목의 개수를 반환합니다.                                          |
| `s.__mul__(n)`       | •      |      | `s * n` — `s`를 `n`번 반복하여 반환합니다.                                     |
| `s.__imul__(n)`      | •      |      | `s *= n` — `s`를 `n`번 반복하여 `s`에 할당합니다.                             |
| `s.__rmul__(n)`      | •      |      | `n * s` — `s`를 `n`번 반복합니다 (역방향 곱셈).                                |
| `s.pop([p])`         | •      |      | 위치 `p`의 항목 또는 생략 시 마지막 항목을 제거하고 반환합니다.                 |
| `s.remove(e)`        | •      |      | `e`의 첫 번째 항목을 제거합니다.                                              |
| `s.reverse()`        | •      |      | 리스트를 제자리에서 뒤집습니다.                                               |
| `s.__reversed__()`   | •      |      | 리스트의 마지막에서 첫 번째 항목까지의 반복자를 반환합니다.                    |
| `s.__setitem__(p, e)`| •      |      | 위치 `p`의 항목을 `e`로 설정합니다.                                           |
| `s.sort([key, reverse])` | •  |     | 리스트를 정렬하며, 선택적으로 `key` 함수와 `reverse` 순서를 사용할 수 있습니다. |
| `s.tobytes()`        |        | •    | 배열을 바이트 객체로 반환합니다.                                              |
| `s.tofile(f)`        |        | •    | 배열을 기계 값으로 파일 `f`에 작성합니다.                                     |
| `s.tolist()`         |        | •    | 배열을 리스트로 변환합니다.                                                   |
| `s.typecode`         |        | •    | 배열의 항목 유형을 나타내는 유형 코드를 반환합니다.                           |



```python

# 커다란 실수 배열의 생성, 저장, 로딩

from array impprt array
from random import random

floats = array('d', (random() for i in range(10**7)))
floats[-1]

# > 0.073258373482

fp = open('floats.bin', 'wb')
floats.tofile(fp) # 배열을 이진 파일에 저장함
fp.close()
floats2 = array('d')
fp = open('floats.bin', 'rb')
floats2.fromfile(fp, 10**7) # 이진 파일에서 천만 개의 숫자를 읽어옴
fp.close()
float2[-1]

# > 0.073258373482

floats2 == floats

# > True

```

> - 리스트 안에 숫자마 들어 있는 경우 배열이 리스트보다 더 효율적임
> - 파이썬 배열은 C 배열만큼 가벼움. 배열을 생성할 때는 배열에 저장되는 각 항목의 C 기반 형을 결정하는 문자인 타입코드를 지정함
> - 또한, 숫자가 아주 많이 들어 있는 시퀀스의 경우 배열에 저장하면 메모리가 많이 절약됨.


<br>

#### 👉 메모리 뷰

```python

import array

numbers = array.array('h', [-2, -1, 0, 1, 2]) # 16비트 정수 배열
memv = memoryview(numbers) # 16비트 메모리 뷰 생성 
len(memv)

# > 5

memv[0]

# > -2

memv_oct = memv.cast('B') # 8bit로 잘라서 읽기
memv_oct.tolist()

# > [254, 255, 255, 255, 0, 0, 1, 0, 2, 0]

memv_oct[5] = 4
numbers

# > array('h', [-2, -1, 1024, 1, 2])


```

> - 메모리 뷰 내장 클래스는 공유 메모리 시퀀스형으로서 bytes를 복사하지 않고 배열의 슬라이스를 다룰 수 있게 해줌
> - 즉, 메모리를 어떻게 볼건가. 배열의 기본 단위를 어떻게 쪼갤 것인가에 대한 것
> - 다시 말해서, 모든 배열은 byte 배열이지만 이것을 어떤 단위로 쪼개서 사용할 것인가를 정하는 것이 메모리뷰임

<br>

#### 👉 NumPy와 SciPy

```python

import numpy

a = numpy.arange(12)
a
# > array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11])

type(a)
# > <class 'numpy.ndarray'>

a.shape = 3, 4
a
# > array([[0, 1, 2, 3],
# >        [4, 5, 6, 7],
# >        [8, 9, 10, 11]])

a[2]
# > array([8, 9, 10, 11])

a[2, 1]
# > 9

a[:, 1]
# > array([1, 5, 9])

a.transpose() # 행과 열을 맞바꿈
# > array([[0, 4, 8],
#          [1, 5, 9],
#          [2, 6, 10],
#          [3, 7, 11]])

# 이외에 여러 예제는 추후에 학습해보기 

```

> - NumPy와 SciPy가 제공하는 고급 배열 및 행렬 연산 덕분에 파이썬이 과학 계산 애플리케이션에서 널리 사용됨
> - NumPy는 숫자뿐만 아니라 사용자 정의 레코드도 저장할 수 있는 다차원 동형 배열 및 행렬을 구현하고 요소 단위에서 효율적으로 연산할 수 있게해줌
> - SciPy는 NumPy를 기반으로 작성된 라이브러리로서, 선형대수, 수치해석, ... 여러 과학 계산 알고리즘을 제공함


<br>

#### 👉 덱 및 기타 큐

| 메서드                 | 리스트 | 덱  | 설명                                                        |
|------------------------|--------|------|-------------------------------------------------------------|
| `s.__add__(s2)`        | ●      |      | `s + s2` — 연결한다.                                         |
| `s.__iadd__(s2)`       | ●      | ●    | `s += s2` — 연결한 후 `s`에 저장한다.                        |
| `s.append(e)`          | ●      | ●    | 마지막 항목 오른쪽에 요소 하나를 추가한다.                    |
| `s.appendleft(e)`      |        | ●    | 첫 번째 항목 왼쪽에 요소 하나를 추가한다.                    |
| `s.clear()`            | ●      | ●    | 모든 항목을 제거한다.                                        |
| `s.__contains__(e)`    | ●      | ●    | `e in s`                                                    |
| `s.copy()`             | ●      | ●    | 목록을 얕게 복사한다.                                       |
| `s.__copy__()`         | ●      | ●    | `copy.copy()` 지원(얕은 복사)                                |
| `s.count(e)`           | ●      | ●    | `e` 요소가 발생한 횟수를 반환한다.                           |
| `s.__delitem__(p)`     | ●      | ●    | `p` 위치의 항목을 삭제한다.                                  |
| `s.extend(i)`          | ●      | ●    | 반복 가능한 `i`에 있는 요소를 오른쪽에 추가한다.             |
| `s.extendleft(i)`      |        | ●    | 반복 가능한 `i`에 있는 요소를 왼쪽에 추가한다.               |
| `s.__getitem__(p)`     | ●      | ●    | `s[p]` — `p` 위치의 항목을 가져온다.                         |
| `s.index(e)`           | ●      | ●    | 처음 `e`가 나타난 위치를 반환한다.                           |
| `s.insert(p, e)`       | ●      |      | `p` 위치의 항목 앞에 `e` 요소를 추가한다.                    |
(추후에 101페이지 표 추가해주기)


```python

from collections import deque

dq = deque(range(10), maxlen=10)
dq

# > deque([0, 1, 2, 3, 4, 5, 6, 7, 8, 9], maxlen=10)

dq.rotate(3)
dq

# > deque([7, 8, 9, 0, 1, 2, 3, 4, 5, 6], maxlen=10)

dq.rotate(-4)
dq

# > deque([1, 2, 3, 4, 5, 6, 7, 8, 9, 0], maxlen=10)

dq.appendleft(-1)
dq

# > deque([-1, 1, 2, 3, 4, 5, 6, 7, 8, 9], maxlen=10)
```


> - 덱(collections.deque) 클래스는 큐의 양쪽 어디에서든 빠르게 삽입 및 삭제할 수 있도록 설계된 스레드 아전한 양방향 큐임
> - 덱은 최대 길이를 설정해서 제한된 항목만 유지할 수도 있으므로 덱이 꽉 찬 후에는 새로운 항목을 추가할 때 반대쪽 항목을 버림
> - 덱은 단점도 있음, 덱의 중간 항목을 삭제하는 연산은 그리 빠르지 않음. 덱이 양쪽 끝에 추가나 제거하는 연산에 최적화 되어 있기 때문임

<br>

#### 👉 요약

> - 파이썬 시퀀스는 가변형, 불변형으로 구분하고 균일 시퀀스와 컨테이너 시퀀스로 구분함
> - 지능형 리스트와 제너레이터 표현식은 시퀀스를 생성하고 초기화하는 강력한 표기법임
> - 또한, 파이썬에서 제공하는 튜플은 익명 필드를 가진 레코드 및 불변 리스트로 사용할 수 있음
> - 시퀀스 슬라이싱도 있음



<br>
<br>



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

