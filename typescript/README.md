# TypeScript

## 💡 What I Learned
### 목차
- [기본 타입](#기본-타입)
- [Interface](#Interface) 
- [Class](#Class)  
  - [access modifier](#Access-modifier)
  - [readonly](#readonly)
  - [static](#static)
  - [getter/setter](#getter/setter)
  - [inheritance](#inheritance)
  - [abstract class](#abstract-class)
---

### 기본 타입
- `Boolean`, `Number`, `String`, `Object`, `Array`, `Tuple`, `Enum`, `Any`, `Void`, `Null`, `Undefined`, `Never`

  ```typescript
  let isDone: boolean = false;
  let decimal: number = 6;
  let color: string = "blue";
  let employee: object;
  employee = {
      name: gildong,
      age: 23,
      jobTitle: 'Web Developer'
  };
  let arr: number[] = [1, 2, 3];
  let arr: Array<number> = [1, 2, 3];
  let tuple: [string, number] = ['hi', 10];
  enum Direction {
    Up,
    Down,
    Left,
    Right,
  }
  let notSure: any = 4;
  notSure = 'maybe a string instead';
  notSure = false;
  function warnUser(): void {
    console.log('This is my warning message');
  }
  // null과 undefined는 다른 모든 타입의 하위 타입
  let u: undefined = undefined;
  let n: null = null;
  // never 타입은 절대 발생할 수 없는 타입
  // never는 함수 표현식이나 화살표 함수 표현식에서 항상 오류를 발생시키거나 절대 반환하지 않는, 끝에 도달하지 않는 타입으로 쓰인다.
  function error(message: string): never {
    throw new Error(message);
  }
  ```

### Interface
- 인터페이스는 상호 간에 정의한 약속 혹은 규칙을 의미한다. 

- 타입스크립트에서의 인터페이스는 보통 다음과 같은 범주에 대해 약속을 정의할 수 있다.
  - (1) 객체의 스펙(속성과 속성의 타입)
 
  - (2) 함수의 스펙(파라미터, 반환 타입 등)  
    함수 타입을 인터페이스로 정의하는 경우, 호출 시그니처(Call signature)를 사용한다.  
    호출 시그니처는 다음과 같이 함수의 매개 변수(parameter)와 반환 타입을 지정한다.
    ```typescript
    interface IName {
      (PARAMETER: PARAM_TYPE): RETURN_TYPE // Call signature
    }
    ```
   
  - (3) 배열과 객체를 접근하는 방식
  
  - (4) 클래스 : 인터페이스로 클래스를 정의하는 경우, implements 키워드를 사용한다.
  
- 인터페이스를 인자로 받아 사용할 때 항상 `인터페이스의 속성 개수`와 `인자로 받는 객체의 속성 개수`를 일치시키지 않아도 된다.  
  다시 말해, 인터페이스에 정의된 `속성`, `타입`의 조건만 만족한다면 객체의 속성 개수가 더 많아도 상관없다는 의미다.  
  또한, 인터페이스에 선언된 속성 순서를 지키지 않아도 된다.
  
- ```typescript
  interface 인터페이스_이름 {
    속성?: 타입; // 속성에 ?를 사용하면 선택적 속성으로 정의할 수 있다.
  }
  ```
  
- 일부 프로퍼티들은 객체가 처음 생성될 때만 수정 가능하다. 프로퍼티 이름 앞에 `readonly`를 넣어서 이를 지정할 수 있다.

- 클래스처럼 인터페이스도 확장(extends)이 가능하다.  
  인터페이스 타입이 클래스 타입을 extends하면, 클래스의 멤버는 상속받지만 구현은 상속받지 않는다.
  
### Class
- 클래스란 객체를 만들 수 있는 방법
- TypeScript 클래스는 멤버 변수(객체의 프로퍼티)를 미리 선언해 줘야 한다.  
  ```typescript
  class Book {
    // Typescript 클래스는 클래스 몸체에 클래스 프로퍼티를 사전 선언하여야 한다.
    title;
    author;
    pages;

    constructor(title: string, author: string, pages: number) {
        this.title = title;
        this.author = author;
        this.pages = pages;
        this.init();
    }

    static create() { }

    init() { }
  }

  const reference = new Book('한 권으로 정리하는 4차 산업혁명', '최진기', 367);
  console.log(reference);
  ```

- TypeScript의 클래스는 어떤 점에서 좋을까?
  ES6의 기능을 포함하면서 보다 강력한 기능을 제공함  
  👉🏻 `access modifier`, `readonly`, `static`, `getter/setter`, `inheritance`, `abstract class`
  
  #### access modifier
  - 접근 제한자를 통해 **접근 가능한 범위를 설정**하고, **각 속성에 데이터 타입을 지정**할 수 있다.
  
  - 클래스 기반 객체 지향 언어가 지원하는 접근 제한자 `public, private, protected`를 지원하며 의미 또한 기본적으로 동일
  
  - 단, 접근 제한자를 명시하지 않았을 때(= 생략했을 때) 다른 클래스 기반 언어의 경우 암묵적으로 protected가 지정되지만, TypeScript에서는 모든 프로퍼티와 메소드에 `public`이 지정된다.
  
  - 접근 제한자를 선언한 프로퍼티와 메소드에 대한 접근 가능성은 아래와 같다.
    | 접근 가능성 | public | protected | private |
    |:--:|:--:|:--:|:--:|
    | 클래스 내부 | O | O | O |
    | 자식 클래스 내부 | O | O | X |
    | 클래스 인스턴스 | O | X | X |
    
  #### readonly
  - 이름에서 쉽게 유추할 수 있듯이 **읽기만 가능**한 프로퍼티를 선언할 때 사용된다.
  - 쉽게 말해 프로퍼티를 위해 사용할 수 있는 `const`인 것이다.
 
  #### static
  - ES6에서는 클래스에 `static` 키워드를 제공하고 있다.  
    하지만 JavaScript의 `static`은 메소드 전용으로, 프로퍼티에는 활용할 수 없는 키워드다.  
    다행히도 TypeScript에서는 `static` 키워드를 **프로퍼티에서도 활용**할 수 있다.
    
  - 인스턴스가 아닌 **클래스 이름으로 호출**한다. (ex. class.property)
  
  - 장점 : 인스턴스 생성 없이 바로 접근 가능하므로 메모리 절약 효과가 있다.

  #### getter/setter
  - JavaScript : 객체의 멤버에 접근할 수 있는 방법으로 ES6의 getter와 setter를 지원한다.  
    클래스 내에 `get`과 `set` 키워드를 통해 getter와 setter를 선언할 수 있다.
  
  - TypeScript : 비공개로 설정할 필요가 있는 속성을 `private`으로 설정한 후,  
    이 속성에 접근해 값을 읽고 쓸 때 `getter, setter` 사용
  
  - 주의 : 함수처럼 호출하면 안 되고, 프로퍼티처럼 조회해야 함  
    `xxx.foo()` → ❌ , `xxx.foo` → ⭕
    
  #### inheritance
  - 타입스크립트에서는 `extends` 키워드를 통해 클래스 상속을 지원한다.
  
  - 상속은 부모 클래스에 정의된 프로퍼티, 메소드를 자식 클래스에서 사용할 수 있게 해주는 기능


  - 자식 클래스의 생성자에서 `super()`를 이용해 상위 클래스의 생성자를 호출해야 하며, 이 메소드는 생략할 수 없다. 
    ```typescript
    class 부모클래스 {
      constructor(a, b, c){}
      ...
    }

    class 자식클래스 extends 부모클래스 {
      constructor() {
        super(a, b, c);
      }
    }
    ```
    
  #### abstract class
  - JavaScript는 추상 클래스 제공 x
  
  - 추상 클래스는 **하나 이상의 추상 메소드를 포함**하며 일반 메소드도 포함할 수 있다.
  
  - 추상 메소드 : **내용 없이** `메소드 이름`과 `타입`만 선언된 메소드. 선언할 때 `abstract` 키워드 사용.
  
  - 추상 클래스를 상속하는 클래스에서는 반드시 추상 클래스의 추상 메소드를 구현해야 한다.
  
  - 추상 클래스를 정의할 때는 class 앞에 abstract라고 표기한다. (`abstract class 클래스명 ...` )
  
  - 추상 클래스는 객체 인스턴스를 생성할 수 없다.
