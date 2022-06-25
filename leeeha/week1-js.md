# 생활코딩 JavaScript 강의 요약 

https://opentutorials.org/course/3085 

- 자바스크립트는 사용자와 상호작용하기 위해 만들어진 언어이다. 
- 웹 브라우저는 한번 화면에 출력되면 자기 자신을 바꿀 수 없다. 하지만 자바스크립트로 html 코드를 제어해서 사용자의 동작에 따라 달라지는 동적인 웹 페이지를 만들 수 있게 된다. 

# 목차 

- [HTML과 JavaScript의 만남](#html과-javascript의-만남)
- [기본 문법](#기본-문법)
- [파일로 쪼개서 정리정돈 하기](#파일로-쪼개서-정리정돈-하기) 
- [jQuery 사용해보기](#jQuery-사용해보기) 

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

### 객체 기본 사용법 

```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
</head>
<body>
    <h1>Object</h1>

    <h2>Create</h2>
    <script>
        /* 객체 생성 */
        var coworkers = {
            "programmer":"egoing",
            "designer":"leezche"
        };

        /* 객체 접근 */
        document.write("programmer: " + coworkers.programmer + "<br>");
        document.write("designer: " + coworkers.designer + "<br>");


        /* 객체 추가 */
        coworkers.bookkeeper = "duru";
        document.write("bookkeeper: " + coworkers.bookkeeper + "<br>");

        coworkers["data scientist"] = "taeho"; /* key 값에 띄어쓰기가 있는 경우 */
        document.write("data scientist: " + coworkers["data scientist"] + "<br>");
    </script>

    <h2>Iterate</h2>
    <script>
        /* 객체 순회 */
        for(var key in coworkers){
            document.write(key + ' : '  + coworkers[key] + '<br>');
        }
    </script>

    <h2>Property & Method</h2>
    <script>
        /* 함수 정의 */
        coworkers.showAll = function(){
            for(var key in this){
                document.write(key + ' : '  + this[key] + '<br>');
            }
        }

        /* 함수 호출 */
        coworkers.showAll();
    </script>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/68090939/175769288-0017bb4d-25a3-4ae8-9c82-f15b5068bb30.png)

### 객체 활용

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

```html
<!DOCTYPE html>
<html>

<head>
    <title>WEB1 - JavaScript</title>
    <meta charset="utf-8">
    <link rel="stylesheet" href="style.css">

    <script>
        function LinksSetColor(color){
            var alist = document.querySelectorAll('a');
            var i = 0;
            while(i < alist.length){
                alist[i].style.color = color;
                i++;
            }
        }

        function BodySetColor(color){
            document.querySelector('body').style.color = color;
        }

        function BodySetBackgroundColor(color){
            document.querySelector('body').style.backgroundColor = color;
        }

        function nightDayHandler(self){
            var target = document.querySelector('body')
            if(self.value === 'night'){
                BodySetBackgroundColor('black');
                BodySetColor('white');
                self.value = 'day';
                LinksSetColor('powderblue');
            }else{ 
                BodySetBackgroundColor('white');
                BodySetColor('black');
                self.value = 'night';
                LinksSetColor('blue');
            }
        }
    </script>
</head>

<body>
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

```html
<!DOCTYPE html>
<html>

<head>
    <title>WEB1 - JavaScript</title>
    <meta charset="utf-8">
    <link rel="stylesheet" href="style.css">

    <script>
        var Body = {
            setColor:function(color){
                document.querySelector('body').style.color = color;
            },
            setBackgroundColor:function(color){
                document.querySelector('body').style.backgroundColor = color;
            }
        }

        var Links = {
            setColor:function(color){
                var alist = document.querySelectorAll('a');
                var i = 0;
                while(i < alist.length){
                    alist[i].style.color = color;
                    i++;
                }
            }
        }

        function nightDayHandler(self){
            var target = document.querySelector('body')
            if(self.value === 'night'){
                Body.setBackgroundColor('black');
                Body.setColor('white');
                self.value = 'day';

                Links.setColor('powderblue');
            }else{ 
                Body.setBackgroundColor('white');
                Body.setColor('black');
                self.value = 'night';

                Links.setColor('blue');
            }
        }
    </script>
</head>

<body>
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

# 파일로 쪼개서 정리정돈 하기 

https://opentutorials.org/course/3085/18856

https://github.com/leeeha/my-first-web-site → 전체 코드 확인! 

https://leeeha.github.io/my-first-web-site/ → GitHub Pages 기능을 이용해서 웹사이트 호스팅한 거 확인!

# jQuery 사용해보기 

https://developers.google.com/speed/libraries#indefinite-observable

`<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>`

https://api.jquery.com/css/ → jQuery 이용해서 css 속성 변경하기 

```html
<head>
    <title>WEB1 - JavaScript</title>
    <meta charset="utf-8">
    <link rel="stylesheet" href="style.css">
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
    <script src="colors.js"></script>
</head>
```

```html
var Body = {
    setColor:function(color){
        //document.querySelector('body').style.color = color;
        $('body').css('color', color);
    },
    setBackgroundColor:function(color){
        //document.querySelector('body').style.backgroundColor = color;
        $('body').css('backgroundColor', color);
    }
}

var Links = {
    setColor:function(color){
        // var alist = document.querySelectorAll('a');
        // var i = 0;
        // while(i < alist.length){
        //     alist[i].style.color = color;
        //     i++;
        // }
        $('a').css('color', color);
    }
}
```
