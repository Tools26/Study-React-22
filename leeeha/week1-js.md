# 생활코딩 JavaScript 강의 요약 

https://opentutorials.org/course/3085 

- 자바스크립트는 사용자와 상호작용하기 위해 만들어진 언어이다. 
- 웹 브라우저는 한번 화면에 출력되면 자기 자신을 바꿀 수 없다. 하지만 자바스크립트로 html 코드를 제어할 수 있다! 사용자의 동작에 따라 달라지는 동적인 웹 페이지를 만들 수 있는 것이다! 

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







