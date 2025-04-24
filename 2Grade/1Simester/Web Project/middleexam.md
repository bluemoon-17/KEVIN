# ✅ 1번째 코드 분석 
<%@ page import="java.time.LocalDateTime" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" trimDirectiveWhitespaces="true" %>
<%
    LocalDateTime now = LocalDateTime.now();
%>
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>타이틀</title>
</head>
<body>
<h1>Hello JSP</h1>
<p style="color: red;">현재시간: <%= now %></p>
</body>
</html>
📌 특징 요약

## 요소	설명
**<%@ page import %>**	Java 클래스 java.time.LocalDateTime을 불러와서 현재 시간 처리에 사용
**<%@ page contentType %>**	HTML 문서의 인코딩 지정 (UTF-8)
**<%@ page ... trimDirectiveWhitespaces %>**	JSP 출력 시 공백을 자동 제거 (성능 및 포맷 개선용)
**<% ... %>	스크립트릿(Scriptlet)** 사용: Java 코드를 JSP 내에 직접 작성
**<%= now %>**	현재 시간을 출력하는 표현식(Expression)
## 📙 책에서 설명하는 포인트:

JSP 파일 내에서 Java 코드를 사용할 때는 스크립트릿(Scriptlet) 을 사용할 수 있지만, MVC 구조로 발전해갈수록 JSTL이나 EL(Expression Language) 사용을 권장함.

LocalDateTime.now()를 통해 실시간 데이터를 JSP에서 출력하는 예는 동적인 웹 페이지 작성을 보여주는 전형적인 사례.

## 🧩 코드 1 - 현재 시간 출력

| 항목 | 설명 |
|------|------|
| 주요 목적 | 현재 시간 출력 |
| 사용 기술 | **스크립틀릿 (`<% %>`), 표현식 (`<%= %>`), `java.time.LocalDateTime`** |
| 핵심 개념 | - **스크립틀릿**: JSP에서 자바 코드 삽입<br> - **표현식**: 값 출력<br> - **지시어 import**를 통해 외부 클래스 활용 |
| 관련 도서 장 | 2장 JSP 기초 문법 |


# ✅ 2번째 코드 분석
<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<!DOCTYPE html>
<html>
<head>
    <title>JSP - Hello World</title>
</head>
<body>
<h1><%= "Hello World!" %></h1>
<br/>
<a href="hello-servlet">Hello Servlet</a>
</body>
</html>
📌 특징 요약

## 요소	설명
<%@ page contentType ... pageEncoding %>	HTML 인코딩 및 페이지 인코딩 설정
<%= "Hello World!" %>	JSP 표현식(Expression)으로 문자열 출력
<a href="hello-servlet">	다른 서블릿 페이지로 연결 (컨트롤러 역할)
## 📙 책에서 설명하는 포인트:

JSP의 가장 기본적인 구조를 보여주는 예시.

표현식 <%= %> 을 이용해 간단한 문자열 출력.

hello-servlet 링크는 MVC 패턴의 Controller(Servlet) 와 연결됨을 시사.

## 🧩 코드 2 - Hello World + 링크

| 항목 | 설명 |
|------|------|
| 주요 목적 | 정적 텍스트 출력 + 서블릿 링크 제공 |
| 사용 기술 | **표현식**, **하이퍼링크 (`<a href>`)** |
| 핵심 개념 | - **정적/동적 콘텐츠 혼합**<br> - **페이지 간 이동 구성** |
| 관련 도서 장 | 2장 JSP와 HTML 통합 |

# 4주차

## ✅ 📄 1번 코드 – 기본 출력 + 서블릿 링크 연결
<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<!DOCTYPE html>
<html>
<head>
  <title>JSP - Hello World</title>
</head>
<body>
<h1><%= "Hello World!" %></h1>
<br/>
<a href="hello-servlet">Hello Servlet</a>
</body>
</html>
### 📌 핵심 포인트
JSP 표현식 <%= %> 사용: 간단한 출력 ("Hello World!")

서블릿과 연결된 링크: hello-servlet

JSP의 기본 구조와 서블릿 연동 흐름을 보여주는 기초 예제

## ✅ 📄 2번 코드 – GET/POST 전송 및 로그인 폼 처리
jsp
복사
편집
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
...
<a href="exam01Get.jsp">GET 방식 전송</a>
<form method="post" action="exam01Post.jsp"> ... </form>
### 📌 핵심 포인트
GET 방식 링크 + POST 방식 폼 둘 다 포함

HTML 폼을 통해 사용자 입력(아이디/비밀번호) 받기

exam01Post.jsp에 데이터를 전송 → 4번 코드와 연동

CSS로 input:focus 효과 부여

### 📙 책에서는 클라이언트 입력과 서버로의 요청 처리 흐름을 강조하며 설명

## 🧩 코드 3 - 로그인 폼(GET/POST)

| 항목 | 설명 |
|------|------|
| 주요 목적 | 사용자 로그인 정보 입력 |
| 사용 기술 | **HTML Form**, **POST 방식**, **입력 유효성(required)** |
| 핵심 개념 | - **폼 전송 구조 이해**<br> - **GET vs POST 전송 방식 차이** |
| 관련 도서 장 | 5장 클라이언트 요청 처리 |

## ✅ 📄 3번 코드 – 요청 정보(GET 방식) 확인
<%
  String methodName = request.getMethod();
  String ip = request.getRemoteAddr();
%>
### 📌 핵심 포인트
서버에 요청한 방식(GET/POST)과 클라이언트 IP 주소 확인

request 내장 객체 사용: JSP의 중요한 개념

폼 요청 이후 서버에서 데이터 확인하는 기본 로직

### 📙 책에서는 JSP 내장 객체 중 request를 이용한 처리 흐름을 자세히 설명

## ✅ 📄 4번 코드 – POST 로그인 처리 & 조건문 처리
jsp
복사
편집
String userId = request.getParameter("userId");
String userPassword = request.getParameter("userPassword");
...
if ("admin".equals(userId) && "1234".equals(userPassword)) ...
### 📌 핵심 포인트
request.getParameter()로 폼 데이터 받기

로그인 검증 (admin, 1234) 후 결과에 따라 JS로 분기 처리

JSP 내 조건문(<% if ... %>) 활용

### 📙 책에서는 로그인 인증 로직을 JSP에서 처리하는 기본 구조를 설명하고, → MVC로 넘어가면서 이런 로직은 서블릿(Controller) 으로 옮기라고 안내함

## 🧩 코드 4 - 로그인 처리

| 항목 | 설명 |
|------|------|
| 주요 목적 | 사용자 로그인 검증 |
| 사용 기술 | **request.getParameter()**, **조건문(`if`)**, **자바스크립트 alert** |
| 핵심 개념 | - **파라미터 수신 및 검증**<br> - **조건문을 활용한 흐름 제어**<br> - **동적 JavaScript 출력** |
| 관련 도서 장 | 6장 요청 파라미터 처리, 8장 조건문 처리 |

# 5-1

## ✅ 📄 1번 코드 – 생년월일 선택 폼 (Select + 반복문)
<select name="year">
    <%for (int i = 1900; i <= 2025; i++) {%>
        <option value="<%=i%>"><%=i%></option>
    <%}%>
</select>
📌 핵심 기능
반복문(for) 을 사용해 select 태그 안의 옵션을 생성

연도(19002025), 월(112), 일(1~31)까지 자동으로 생성

서버 사이드에서 동적 HTML 생성하는 기본 예제

제출 기능은 없음 (단순 출력용)

### 📙 관련 챕터: JSP 기본 문법, 표현식 & 스크립틀릿 활용

## 🧩 코드 5 - 생년월일 선택

| 항목 | 설명 |
|------|------|
| 주요 목적 | 생년월일을 선택할 수 있는 select box 구성 |
| 사용 기술 | **반복문(for)**, **스크립틀릿**, **HTML select-option** |
| 핵심 개념 | - **반복문을 통한 동적 옵션 생성**<br> - **입력용 폼 구성의 기초** |
| 관련 도서 장 | 4장 JSP 스크립트 요소 |


## ✅ 📄 2번 코드 – 구구단 출력 프로그램 (폼 처리 + 결과 표시)
jsp
복사
편집
<form method="get" action="gugudan.jsp">
    <select name="dan">
        <option>선택</option>
        <%for (int i = 2; i <= 19; i++) {%>
        <option value="<%=i%>" <%= i == danValue ? "selected" : ""%>  ><%=i%>단</option>
        <%}%>
    </select>
</form>
...
<%for (int i = 1; i <= 19; i++) {%>
    <p><%="%d * %d = %d".formatted(danValue, i, danValue* i)%></p>
<%}%>
### 📌 핵심 기능
GET 방식 폼 제출로 구구단 단수(dan) 전송

선택된 값 유지 (selected 처리)

선택한 단의 구구단 결과 출력

HTML + JSP가 합쳐진 전형적인 동적 페이지

### 📙 관련 챕터:

폼 처리 (request.getParameter 사용)

selected 유지

반복문과 조건문 혼합

## 🧩 코드 6 - 구구단 출력

| 항목 | 설명 |
|------|------|
| 주요 목적 | 구구단 출력 및 선택 유지 |
| 사용 기술 | **GET 폼 전송**, **조건문 + 반복문**, **request.getParameter()**, **selected 속성 유지** |
| 핵심 개념 | - **전송된 값 처리 및 결과 출력**<br> - **사용자 선택값 유지 처리** |
| 관련 도서 장 | 7장 조건문과 반복문 활용 |


## ✅ 📄 3번 코드 – 링크 연결 (메뉴 역할)
<a href="gugudan.jsp">구구단 출력 프로그램</a> |
<a href="birth.jsp">생년월일 프로그램</a>
### 📌 핵심 기능
다른 JSP 페이지로 이동하는 메뉴 역할

gugudan.jsp, birth.jsp로 연결되는 구조

단순 링크이지만, 페이지 간 흐름 설계의 시작점이 될 수 있음

### 📙 관련 챕터: 하이퍼링크 처리, 프로젝트 구조 잡기

## 🧩 코드 7 - 메뉴 페이지

| 항목 | 설명 |
|------|------|
| 주요 목적 | 다른 JSP 페이지로 이동 |
| 사용 기술 | **하이퍼링크 (`<a href>`)** |
| 핵심 개념 | - **페이지 연결 구성** |
| 관련 도서 장 | 3장 JSP 프로젝트 구성 |


# 📌 중복 개념 요약 (최초 언급 기준)

| 개념 | 설명 |
|------|------|
| **스크립틀릿 (`<% %>`)** | JSP 내부에 자바 코드를 삽입하는 구문 |
| **표현식 (`<%= %>`)** | 값을 JSP에서 출력 |
| **request.getParameter()** | 클라이언트로부터 전달된 값 수신 |
| **조건문 / 반복문** | 자바 기반 흐름 제어 구문 |
| **HTML Form** | 사용자 입력 수집 구조 |
| **하이퍼링크 (`<a href>`)** | 페이지 간 이동 구성 |
| **selected 속성 유지** | 드롭다운에서 사용자 선택 유지 |
