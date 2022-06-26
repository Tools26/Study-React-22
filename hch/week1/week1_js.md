# Java 와 Javascript
공통적으로 둘 모두 C 언어의 기본 구문에 바탕을 두었다.
C 언어의 기본 구문에 바탕을 두엇을 뿐이지 두 언어는 직접적인 연관성은 약하다.

# Javascript
objective base script programming language
Web browser 에서 주로 작동, 다른 응용 프로그램의 내장 객체에도 접근할 수 있는 기능을 가짐.
최근에 Node.js 와 같은 runtime 환경 과 같이 server programming에서도 사용되고있다.

# Javascript 기초적인 문법
속성과 메소드를 갖는 객체(obejct) 개념이 있으며, 변수 선언, 함수 정의, 연산자 그리고 제어문 등을 이 프로그래밍 언어의
주요 개념으로 언급할 수 있을뿐만 아니라 이 언어가 속한 객체 지향 프로그래밍언어의 공통적인 주요 개념이기도 하다.

# 변수 선언
기본적으로 C나 Java 등 타 언어에서는 변수를 선언할때, 형태를 정해준다. 예를들어 Integer, Double, Boolean 등이 있는데,
JavaScript에서는 변수를 선언 할 때, let var const 등이 사용된다.
즉,  Int 형 3 과 String 형 '3' 이 있다 가정한다.
3 과 '3' 을 더한다면 어떻게 될까.

JavaScript는 Dynamic Typing 기능을 가지고 있기 때문에
3 + '3' 을 진행한다면 Javascript는 6을 반환한다.

## Dynamic Typing 
Dynamic Typing은 Code를 작성하는데 있어서 컴퓨터적 구조를 생략한다.
따라서 변수를 지정할 때 해당 변수의 데이터 타입 등을 명시하지 않아도 컴퓨터가 알아서 해석하도록 한다.
장점 : 코드를 간결하게 해주어 로직을 보다 명확히 보여줄 수 있다.
단점 : Data Type이 뭔지 파악하는 것을 전적으로 컴퓨터에게 맡기기 때문에 그 만큼 실행속도가 느려진다.

Dynamic Typing, Static Typing 출처 :https://seongonion.tistory.com/16

# JavaScript with ECMAScript
Javascript는 ECMAScript의 표준 사양을 가장 잘 구현한 언어
~ES5까지는 대부분의 브라우저에서 기본적으로 지원되었지만
ES6 이후부터는 브라우저 호환성을 위해 트랜스파일러로 컴파일된다.

## 트랜스파일러 (Transpiler)
프로그래밍 언어로 작성된 프로그램의 소스 코드를 입력받아 다른 프로그래밍 언어로 동등한 소스 코드를
만들어내는 Compiler의 일종.
트랜스컴파일된 언어의 예로는 클로저 컴파일러, 커피스크립트, 다트, Haxe, Typescript, Emscripten 이 포함된다.