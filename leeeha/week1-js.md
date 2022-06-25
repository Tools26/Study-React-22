# 생활코딩 JavaScript 강의 요약 

https://opentutorials.org/course/3085 

- 자바스크립트는 사용자와 상호작용하기 위해 만들어진 언어이다. 
- 웹 브라우저는 한번 화면에 출력되면 자기 자신을 바꿀 수 없다. 하지만 자바스크립트로 html 코드를 제어해서 사용자의 동작에 따라 달라지는 동적인 웹 페이지를 만들 수 있게 된다. 

# 목차 

- [HTML과 JavaScript의 만남](#html과-javascript의-만남)
- [기본 문법](#기본-문법)
- [라이브러리와 프레임워크](#라이브러리와-프레임워크)
- [UI vs API](#ui-vs-api)

# HTML과 JavaScript의 만남 

## script 태그

기본적으로 자바스크립트는 html 위에서 동작하는 언어이다. 즉, 웹 브라우저에게 자바스크립트 코드라는 걸 알려주려면 script 태그를 사용하면 된다! 

```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <title>JavaScript</title>
</head>
<body>
    <h1>Hello World</h1>
    <script>
        document.write(1+1); /* 동적 */
    </script>

    <h1>Hello World</h1>
    1+1 /* 정적 */
</body>
</html>
```

![image](https://user-images.githubusercontent.com/68090939/175760029-18695f8f-2ee6-4119-8149-5e551cff809f.png)

## 이벤트 

```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
</head>
<body>
    <input type="button" value="hi" onclick="alert('hi')">
    <input type="text" onchange="alert('changed!')">
    <input type="text" onkeydown="alert('key down!')">
</body>
</html>
```

![image](https://user-images.githubusercontent.com/68090939/175760369-04048fee-8bb5-4f19-9c30-631d368b6f80.png)

## 콘솔

![image](https://user-images.githubusercontent.com/68090939/175760693-d915231c-044e-4812-90fd-2b0423d087fd.png)

개발자 도구의 콘솔 창에서 자바스크립트 코드를 바로 실행할 수도 있다! 새로운 웹페이지를 제작하는 것뿐만 아니라, 기존에 존재하는 웹 페이지의 요소를 분석할 때도 자바스크립트가 유용하게 사용될 수 있는 것이다. 

# 기본 문법 

## 데이터 타입 

아래 사진은 문자열과 숫자 각각에 산술 연산자를 적용한 결과이다. 따라서 데이터 타입을 잘 구분해서 사용할 필요가 있다! 

![image](https://user-images.githubusercontent.com/68090939/175761223-6b27efd1-f4ca-466c-bf4c-5c444ccd963d.png)

[String의 다양한 메소드가 궁금하다면 클릭!](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)


## 제어할 태그 선택하기 

javascript select tag by css selector 

https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector#examples 

```html
<!DOCTYPE html>
<html>

<head>
    <title>WEB1 - JavaScript</title>
    <meta charset="utf-8">
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <input type="button" value="night" onclick=" 
        document.querySelector('body').style.backgroundColor = 'black';
        document.querySelector('body').style.color = 'white';
    ">

    <input type="button" value="day" onclick="
        document.querySelector('body').style.backgroundColor = 'white';
        document.querySelector('body').style.color = 'black';
    ">

    <h1><a href="index.html">WEB</a></h1>

    <div id="grid">
        <ol>
            <li><a href="1.html">HTML</a></li>
            <li><a href="2.html">CSS</a></li>
            <li><a href="3.html">JavaScript</a></li>
        </ol>
        <div id="article">
            <h2>JavaScript</h2>
            <p>
                JavaScript, often abbreviated JS, is a programming language that is one of the
                core technologies of the World Wide Web, alongside HTML and CSS.[11] As of 2022, 98% of websites use
                JavaScript on the client side for web page behavior,[12] often incorporating third-party libraries.[13]
                All major web browsers have a dedicated JavaScript engine to execute the code on users' devices.
            </p>
        </div>
    </div>
</body>

</html>
```

![image](https://user-images.githubusercontent.com/68090939/175762441-337c8310-fedb-4e9f-8afb-3d9ceb4f1c7b.png)

![image](https://user-images.githubusercontent.com/68090939/175762444-36e8a2a8-2da4-4cf4-9590-d15978c30f6c.png)

body 태그 안에 아래의 자바스크립트 코드 삽입해서, 사용자의 입력(클릭)에 대한 이벤트 처리를 할 수 있게 되었다! 

```html
 <input type="button" value="night" onclick=" 
    document.querySelector('body').style.backgroundColor = 'black';
    document.querySelector('body').style.color = 'white';
">

<input type="button" value="day" onclick="
    document.querySelector('body').style.backgroundColor = 'white';
    document.querySelector('body').style.color = 'black';
">
``` 

## 리팩토링 

```html
<input id="night_day" type="button" value="night" onclick="
    if(document.querySelector('#night_day').value === 'night'){
        document.querySelector('body').style.backgroundColor = 'black';
        document.querySelector('body').style.color = 'white';
        document.querySelector('#night_day').value = 'day';
    }else{
        document.querySelector('body').style.backgroundColor = 'white';
        document.querySelector('body').style.color = 'black';
        document.querySelector('#night_day').value = 'night';
    }
">
```

위의 코드를 더 간결하게 바꿔보자! 동일한 버튼을 1억개 만들어야 하는, 극단적인 상황을 가정해서 생각해보면 중복된 코드들을 왜 없애야 하는지 이해할 수 있을 것이다. 

```html
<input type="button" value="night" onclick="
    /* 같은 단어를 모두 선택하는 단축키: Ctrl + Shift + L */
    var target = document.querySelector('body')
    if(this.value === 'night'){
        target.style.backgroundColor = 'black';
        target.style.color = 'white';
        this.value = 'day';
    }else{
        target.style.backgroundColor = 'white';
        target.style.color = 'black';
        this.value = 'night';
    }
">
```

## 배열과 반복문으로 a 태그의 style 속성 값 바꾸기 

```html
<input type="button" value="night" onclick="
    var target = document.querySelector('body')
    if(this.value === 'night'){
        target.style.backgroundColor = 'black';
        target.style.color = 'white';
        this.value = 'day';

        var alist = document.querySelectorAll('a');
        var i = 0;
        while(i < alist.length){
            alist[i].style.color = 'powderblue';
            i++;
        }
    }else{ 
        target.style.backgroundColor = 'white';
        target.style.color = 'black';
        this.value = 'night';

        var alist = document.querySelectorAll('a');
        var i = 0;
        while(i < alist.length){
            alist[i].style.color = 'blue';
            i++;
        }
    }
">
```

![image](https://user-images.githubusercontent.com/68090939/175765100-a2f147f2-ced5-4b2b-856b-209e2f90a6a9.png)

![image](https://user-images.githubusercontent.com/68090939/175765107-95a28a41-fa1c-461e-b43f-baca8b2b8b1e.png)

## 함수 

```html
<!DOCTYPE html>
<html>

<head>
    <title>WEB1 - JavaScript</title>
    <meta charset="utf-8">
    <link rel="stylesheet" href="style.css">

    <script>
        function nightDayHandler(self){
            var target = document.querySelector('body')
            if(self.value === 'night'){
                target.style.backgroundColor = 'black';
                target.style.color = 'white';
                self.value = 'day';

                var alist = document.querySelectorAll('a');
                var i = 0;
                while(i < alist.length){
                    alist[i].style.color = 'powderblue';
                    i++;
                }
            }else{ 
                target.style.backgroundColor = 'white';
                target.style.color = 'black';
                self.value = 'night';

                var alist = document.querySelectorAll('a');
                var i = 0;
                while(i < alist.length){
                    alist[i].style.color = 'blue';
                    i++;
                }
            }
        }
    </script>
</head>

<body>
    <input id="night_day" type="button" value="night" onclick="
        nightDayHandler(this);
    ">

    <input id="night_day" type="button" value="night" onclick="
        nightDayHandler(this);
    ">

    <h1><a href="index.html">WEB</a></h1>

    <div id="grid">
        <ol>
            <li><a href="1.html">HTML</a></li>
            <li><a href="2.html">CSS</a></li>
            <li><a href="3.html">JavaScript</a></li>
        </ol>
        <div id="article">
            <h2>JavaScript</h2>
            <p>
                JavaScript, often abbreviated JS, is a programming language that is one of the
                core technologies of the World Wide Web, alongside HTML and CSS.[11] As of 2022, 98% of websites use
                JavaScript on the client side for web page behavior,[12] often incorporating third-party libraries.[13]
                All major web browsers have a dedicated JavaScript engine to execute the code on users' devices.
            </p>
        </div>
    </div>
</body>

</html>
```

중복을 제거하는 데 효과적인 함수! 

## 객체 



# 라이브러리와 프레임워크 

# UI vs API 








