# 생활코딩 HTML/CSS/JS 요약 

기초 강의이기 때문에 모든 내용을 자세히 필기하지는 않고, 실습 위주로 강의를 들었다! 

# 목차 

- [HTML (Hypertext Markup Language)](#html) 
- [CSS (Cascading Style Sheets)](#css) 
- [JavaScript](#javascript) 

# HTML 

## 태그와 속성 

![image](https://user-images.githubusercontent.com/68090939/175207281-e9d2506d-75bb-4640-a698-835f288566d5.png)

- strong (볼드체), u (밑줄)
- h1~6 (제목)
- br (줄바꿈), p (단락) 
- li (리스트), ol (ordered list), ul (unordered list)
- table, tr (행), td (열)
- title (웹사이트의 표지) 
- meta (utf-8로 읽으라고 웹브라우저에게 알려줌) 
- html, head, body 

📌 **인상 깊었던 내용**: https://opentutorials.org/course/3084/18488

>의미에 맞는 태그로 웹페이지를 만든 지식인과 그렇지 않은 일반인은 10년 뒤에 인생이 달라져 있을 것입니다. **웹의 핵심적인 철학은 접근성입니다.** 
**웹은 모든 운영체제에서 동작하고, 웹페이지의 소스코드는 누구나 볼 수 있고, 웹은 저작권이 없는 순수한 공공재입니다.** 웹의 이런 특징들이 웹을 다른 기술들과 구별되는 특별한 것으로 만든다고 생각합니다. 
거기에 더해서 **누구나 차별없이 정보에 접근할 수 있어야 한다는 철학을 접근성(accessibility)라고 합니다.**
특히 웹이 중요하게 생각하는 접근성은 신체적인 장애가 있는 사람도 웹을 통해서 정보에 접근할 수 있어야 한다는 것입니다. 
예를 들어서 시각장애가 있는 사람은 스크린리더(screen reader)와 같은 프로그램을 이용해서 정보를 청각화해서 접하게 됩니다. 
그런데 웹페이지를 예쁘게 하기 위해서 HTML을 사용하지 않고 웹페이지 전체를 이미지로 만든다면 시각 장애가 있는 분들에게는 암흑과도 같은 상태가 됩니다. 
**자신도 모르는 사이에 누군가를 소외시키고 있는 것입니다. 반대로, HTML을 의미론적으로 잘 사용한다면 자신도 모르는 사이에 누군가에게 정말 큰 도움을 주고 있는 것입니다. 
이렇게 HTML은 비즈니스적인 측면에서도 중요하지만, 휴머니즘적인 측면에서도 중요한 기술입니다.**

## 서버와 클라이언트 

- 서버 (Server): 서비스를 제공하는 사람 
- 클라이언트 (Client): 정보를 받는 고객 

## 웹호스팅 

- 호스트: 인터넷에 연결된 컴퓨터 하나하나 
- 호스팅, 클라우드: 이런 컴퓨터들을 빌려주는 기술 

📌 **알고 있는 것을 공고히 하는 두 가지 방법**
>1. 알고 있는 지식을 이용해 프로젝트를 만들어본다. 
>2. 알고 있는 지식을 컨텐츠로 만들어서 누군가에게 알려준다. 
>
>→ 내가 무엇을 알고 있는지를 자신과 타인에게 확인시켜 줄 수 있는 너무나도 중요한 방법!!! 

# CSS 

HTML은 정보를, CSS는 디자인을 담당한다! CSS로 디자인 관련된 코드를 한번에 처리하므로 HTML에서 비효율적으로 중복되는 코드를 제거할 수 있다. 즉, 유지보수가 편리해진다! 

(항상 극단적인 상황을 가정해볼 것! 동일한 코드가 10억개 이상 중복된다면? CSS라는 새로운 문법이 반드시 필요할 수밖에 없다!) 

<img width="500px" src="https://user-images.githubusercontent.com/68090939/175209234-5b34c938-371b-4562-b324-1ac713dd3c61.png"> 

## Selector의 우선순위 

```html
<!DOCTYPE html>
<html>
    <head>
        <title>WEB1 - CSS</title>
        <meta charset="utf-8">
        <style>
            a {
                color:black;
                text-decoration: none;
            }
            .visited {
                color: gray;
            }
            .active {
                color: red;
            }
            h1 {
                font-size: 45px;
                text-align: center;
            }
        </style>
    </head>
    <body>
        <h1><a href="index.html">WEB</a></h1>
        <ol>
            <li><a href="1.html" class="visited">HTML</a></li>
            <li><a href="2.html" class="visited active">CSS</a></li>
            <li><a href="3.html">JavaScript</a></li>
        </ol>

        <h2>CSS</h2>
        <p>
            CSS specification 
        </p>
    </body>
</html>
```

<img width="500px" src="https://user-images.githubusercontent.com/68090939/175229804-e909884e-eff7-4c8a-8ab2-bd700d917e8e.png">

`<a href="2.html" class="visited active">CSS</a>` 이것처럼 class 속성이 여러 개일 경우 가장 마지막에 나올 수록 우선순위가 더 높다. 그래서 HTML은 회색, CSS는 빨간색으로 표시가 된 것이다. 하지만 이 방법은... 

```html
<!DOCTYPE html>
<html>
    <head>
        <title>WEB1 - CSS</title>
        <meta charset="utf-8">
        <style>
            a {
                color:black;
                text-decoration: none;
            }
            .active {
                color: red;
            }
            .visited {
                color: gray;
            }
            h1 {
                font-size: 45px;
                text-align: center;
            }
        </style>
    </head>
    <body>
        <h1><a href="index.html">WEB</a></h1>
        <ol>
            <li><a href="1.html" class="visited">HTML</a></li>
            <li><a href="2.html" class="visited active">CSS</a></li>
            <li><a href="3.html">JavaScript</a></li>
        </ol>

        <h2>CSS</h2>
        <p>
            CSS specification 
        </p>
    </body>
</html>
```

<img width="500px" src="https://user-images.githubusercontent.com/68090939/175230429-172a9638-a44d-44f4-8de5-038e162d950d.png">

이렇게 active, visited 클래스 선택자의 작성 순서가 바뀌면, body 태그에서 더 가까운 선택자가 우선적으로 적용되어서 CSS가 회색으로 나타난다. 그래서 이것보다 다른 방법을 사용하는 게 좋다! 바로 id 속성을 이용하는 것이다! 

```html
<!DOCTYPE html>
<html>
    <head>
        <title>WEB1 - CSS</title>
        <meta charset="utf-8">
        <style>
            #active { 
                color: red;
            } 
            .visited {
                color: gray;
            }
            a {
                color:black;
                text-decoration: none;
            }
            h1 {
                font-size: 45px;
                text-align: center;
            }
        </style>
    </head>
    <body>
        <h1><a href="index.html">WEB</a></h1>
        <ol>
            <li><a href="1.html" class="visited">HTML</a></li>
            <li><a href="2.html" class="visited" id="active">CSS</a></li>
            <li><a href="3.html">JavaScript</a></li>
        </ol>

        <h2>CSS</h2>
        <p>
            CSS specification 
        </p>
    </body>
</html>
```

<img width="500px" src="https://user-images.githubusercontent.com/68090939/175229804-e909884e-eff7-4c8a-8ab2-bd700d917e8e.png">

이처럼 Selector는 **id(#) > class(.) > tag(element)** 이 순서대로 우선순위가 적용된다. 

왜 그럴까? 무작정 외우지 말고 직관적으로 이유를 생각해보자! 

id는 코드 상에서 한번만 등장하며, 다른 값과 중복되지 않는 유일한 값이기 때문에 우선순위가 가장 높다. 반면에 클래스, 태그는 그보다 더 포괄적이기 때문에 id 선택자보다 우선순위가 낮은 것이다! 

[더 많은 CSS Selector가 궁금하다면 클릭!](https://www.w3schools.com/cssref/css_selectors.asp)

## block level element vs. inline element 

```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <title>Box Model</title>
    <style>
        /* block level element */
        h1{
            border-width: 3px;
            border-color: red;
            border-style: solid;
        }
        /* inline element */
        a{
            border-width: 3px;
            border-color: red;
            border-style: solid;
        }
    </style>
</head>
<body>
    <h1>CSS</h1>
    Cascading Style Sheets (<a href="https://en.wikipedia.org/wiki/CSS">CSS</a>) is a style sheet language 
    used for describing the presentation of a document written in a markup language such as HTML or XML (including XML dialects such as SVG, MathML or XHTML).
</body>
</html>
```

<img width="500px" src="https://user-images.githubusercontent.com/68090939/175247246-0de54015-a6d7-496c-a0e4-d45d4718be84.png">

h1과 같은 block level 태그는 화면 전체를 차지하며 자동으로 줄바꿈이 된다. 반면에 a와 같은 inline 태그는 자기 자신의 콘텐츠만큼만 크기를 차지한다. 

```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <title>Box Model</title>
    <style>
        /* block level element */
        h1{
            border-width: 3px;
            border-color: red;
            border-style: solid;
            display: inline;
        }
        /* inline element */
        a{
            border-width: 3px;
            border-color: red;
            border-style: solid;
            display: block;
        }
    </style>
</head>
<body>
    <h1>CSS</h1>
    Cascading Style Sheets (<a href="https://en.wikipedia.org/wiki/CSS">CSS</a>) is a style sheet language 
    used for describing the presentation of a document written in a markup language such as HTML or XML (including XML dialects such as SVG, MathML or XHTML).
</body>
</html>
```

<img width="500px" src="https://user-images.githubusercontent.com/68090939/175247780-4e0aabab-ffab-489c-ab31-8c17df02cf6a.png">

하지만 display 속성 값에 따라서 차지하는 크기를 다르게 할 수 있다. 그리고 `display: none;`으로 설정하면 해당 태그가 아예 화면에 안 보이게 할 수도 있다! 

```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <title>Box Model</title>
    <style>
        h1, a{
            border:3px solid red; /* 순서는 무관 */
        }
    </style>
</head>
<body>
    <h1>CSS</h1>
    Cascading Style Sheets (<a href="https://en.wikipedia.org/wiki/CSS">CSS</a>) is a style sheet language 
    used for describing the presentation of a document written in a markup language such as HTML or XML (including XML dialects such as SVG, MathML or XHTML).
</body>
</html>
```

중복된 코드를 줄이면 위와 같이 간단해진다! 

## Box Model

<img width="500px" src="https://user-images.githubusercontent.com/68090939/175249986-30cec941-206b-4850-aa4f-afe188842dbd.png">

```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <title>Box Model</title>
    <style>
        h1{
            border:5px solid red;
            padding:20px; /* 안쪽 여백 */
            margin:20px;  /* 바깥 여백 */
            display: block;
            width:100px;
        }
    </style>
</head>
<body>
    <h1>CSS</h1>
    <h1>CSS</h1>
</body>
</html>
```

<img width="500px" src="https://user-images.githubusercontent.com/68090939/175250143-97acde6d-26b8-40d6-b73a-1a71b34c73ab.png">

<img width="500px" src="https://user-images.githubusercontent.com/68090939/175251504-34d6fb3e-25e3-4738-9035-f9fd90246d4b.png">

👉 개발자 도구로 확인해본 모습! 

## Grid 

![image](https://user-images.githubusercontent.com/68090939/175256356-2e7a88ed-96df-44c4-93bc-fd7f1928b4fc.png) 

**div 태그는 block level element**여서 화면 전체를 차지하며 자동 줄바꿈이 된다. 반면에 **span 태그**는 기능이 동일하지만, 자기 자신의 내용만큼만 크기를 차지하는 **inline element**라는 차이점이 있다.

```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <title>Grid</title>
    <style>
        #grid{
            border:5px solid pink;
            display:grid;
            grid-template-columns: 150px 1fr;
        }
        div{
            border:5px solid gray;
        }
    </style>
</head>
<body>
    <div id="grid">
        <div>NAVIGATION</div>
        <div>
            Creative thinking requires our brains to make connections between seemingly unrelated ideas. 
            Is this a skill that we are born with or one that we develop through practice? 
            Let's look at the research to uncover an answer.
        </div>
    </div>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/68090939/175260720-f8f3b341-e2b7-4d56-9c42-92ee398ce946.png)

📌 **유용한 웹 사이트 추천**: https://caniuse.com/ 
> "Can I use" provides up-to-date browser support tables for support of front-end web technologies on desktop and mobile web browsers.

<br> 

### Grid 이용해서 수정한 홈페이지의 모습! 

![image](https://user-images.githubusercontent.com/68090939/175269003-6c12b437-5cb1-4265-84e0-a18c467c01df.png)

```html
<!DOCTYPE html>
<html>
    <head>
        <title>WEB1 - CSS</title>
        <meta charset="utf-8">
        <style>
            body{
                margin: 0;
            }
            h1{
                font-size: 45px;
                text-align: center;
                border-bottom: 1px solid gray;
                margin: 0;
                padding:20px;
            }
            a{
                color:black;
                text-decoration: none;
            }
            #grid{
                display:grid;
                grid-template-columns: 150px 1fr;
            }
            #grid ol{
                border-right:1px solid gray;
                width:100px;
                margin:0;
                padding:20px;
                padding-left:33px;
            }
            #article{
                padding-left: 25px;
            }
        </style>
    </head>
    <body>
        <h1><a href="index.html">WEB</a></h1>
        <div id="grid">
            <ol>
                <li><a href="1.html">HTML</a></li>
                <li><a href="2.html">CSS</a></li>
                <li><a href="3.html">JavaScript</a></li>
            </ol>
            <div id="article">
                <h2>CSS</h2>
                <p>Cascading Style Sheets (CSS) is a style sheet language 
                    used for describing the presentation of a document written in a markup language 
                    such as HTML or XML (including XML dialects such as SVG, MathML or XHTML).[1] 
                    CSS is a cornerstone technology of the World Wide Web, alongside HTML and JavaScript.[2]
                </p>
            </div>
        </div>
    </body>
</html>
```

## 반응형 디자인 

## CSS 코드의 재사용 

# JavaScript 






