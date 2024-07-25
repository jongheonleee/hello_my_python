# 🏊🏻‍♂️ flow_python 🐍

### ⭐️ 목표
> ### 현재 Python의 영향력은 어마어마함
> ### 리눅스까지 들어온 상황임
> ### 즉, Python은 기본중에 기본. 하지만, 더욱 깊이 있게 공부해서 경쟁력을 확보해야함  

<br>
<br>

### 🫵🏻 파이썬 핵심 
> ### 파이썬 철학과 디자인 패턴을 연결할 줄 알아야함
> ### 파이썬으로 OOP 가능해야함. 즉, 설계하고 이를 코드로 녹일 수 있어야함
> ### 깊이있는 책들이 없음, 기존의 자바 및 OOP 개념 총 동원해서 스스로 깊이 있는 학습하는 것이 중요함 

<br>
<br>

### 몰입할 때 참고했던 서적과 교육
> ### 📚 참고 서적 및 사이트
> ### 1. 처음 시작하는 파이썬
> 도서 링크 : https://product.kyobobook.co.kr/detail/S000001810298
> ### 2. 전문가를 위한 파이썬 
> 도서 링크 : https://product.kyobobook.co.kr/detail/S000001057838
> ### 3. 남궁성의 백엔드 데브 캠프 1기(AI 융합)

<br>
<br>

### 📖 파이썬 학습 요약

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
        print("iv가 가변인가? " + self._components is components)

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
        return (len(self) == len(other) and
                all(a == b for a, b in zip(self, other)))

    def __hash__(self):
        hashes = (hash(x) for x in self)
        return functools.reduce(operator.xor, hashes, 0)

    def __abs__(self): 
        """객체의 절대값을 반환하는 함수"""
        return math.sqrt(sum(x * x for x in self))

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

