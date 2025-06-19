# JSP/Java 웹 회원/게시판 시스템 핵심 정리
### 1. DB 연결 - DbConnector.java
MySQL 드라이버 로드

DB 접속 정보(host, port, id, pwd, db) 설정

getConnection() 메서드로 DB 연결 객체(Connection) 반환

### 2. 데이터 모델 (DTO)
BoardDto : 게시글 정보(id, writer, subject, contents, ipAddr, viewCount, createDt, updateDt)

MemberDto : 회원 정보(userId, userName, password, createDt, updateDt)

DashboardDto : 통계 정보(회원수, 게시글수)

### 3. DAO (데이터 접근 객체) - DB 쿼리 수행
BoardDao :

게시글 목록 조회 → getBoardList()

게시글 상세 조회 → getBoard(long boardId)

게시글 추가 → addBoard(BoardDto board)

게시글 수정 → updateBoard(BoardDto board)

MemberDao :

회원 목록 조회 → getMemberList()

회원 상세 조회 → getMember(String userId)

회원 추가 → addMember(MemberDto member)

회원 수정 → updateMember(MemberDto member)

회원 삭제 → deleteMember(String userId)

### 4. 서비스 레이어 (BoardService, MemberService 등)
DAO 호출을 감싸서 실제 비즈니스 로직 처리

JSP에서는 서비스 인터페이스/구현체를 사용해 기능 호출

### 5. JSP 페이지 흐름 및 역할
회원 관련
회원 목록(member-list.jsp)

MemberService 호출해서 회원 리스트 조회 후 테이블 출력

회원 삭제 버튼(삭제 jsp로 이동) 포함

회원 추가(member-add.jsp)

입력폼 제공 (이름, 아이디, 비밀번호)

회원 추가 처리(member-add-submit.jsp)

폼에서 전달된 데이터 MemberDto 생성

MemberService.addMember() 호출 후 성공시 목록 페이지로 리다이렉트

회원 수정(member-edit.jsp)

user_id로 회원 조회 후 폼에 기존 데이터 채워서 수정 가능

회원 수정 처리(member-edit-submit.jsp)

수정 폼 데이터 MemberDto 생성 → MemberService.updateMember() 호출 후 목록으로 이동

회원 삭제 처리(member-delete.jsp)

user_id 받아서 MemberService.deleteMember() 호출 후 목록으로 이동

게시판 관련
게시글 목록(bbs-list.jsp)

BoardService.getBoardList() 호출 후 게시글 테이블 출력

게시글 수정 페이지 링크, 삭제 버튼 포함

게시글 추가(bbs-add.jsp)

게시글 작성 폼 (작성자, 제목, 내용)

게시글 추가 처리(bbs-add-submit.jsp)

폼 데이터 BoardDto 생성 → BoardService.addBoard() 호출 후 목록 이동

게시글 수정(bbs-edit.jsp)

게시글 ID로 상세 조회 후 폼에 기존 데이터 채워서 수정 가능

게시글 수정 처리(bbs-edit-submit.jsp)

폼 데이터 BoardDto 생성 → BoardService.updateBoard() 호출 후 목록으로 이동

로그인/로그아웃
로그인 폼(login.jsp) : 아이디, 비밀번호 입력

로그인 처리(login-submit.jsp)

전달받은 아이디/비밀번호로 로그인 시도 → 성공 시 세션에 userId, userName 저장 후 메인 페이지 이동

실패 시 경고 알림 후 이전 페이지 복귀

로그아웃(logout.jsp)

세션 무효화 후 메인 페이지 이동

공통 UI
include_menu.jsp :

로그인 상태에 따른 메뉴(로그인, 로그아웃) 출력

회원 관리, 게시판 관리, 대시보드 메뉴 제공

include_dashboard.jsp

DashboardService 호출 → 회원수, 게시글수 통계 출력

### 6. 중요 키워드/개념 정리
Connection, PreparedStatement, ResultSet → DB 연결, SQL 실행, 결과 처리

DAO → DB CRUD 기능 담당

DTO → 데이터 전달 객체 (BoardDto, MemberDto)

Service → DAO 호출 및 비즈니스 로직 처리

JSP → 사용자 입력/출력 화면 및 데이터 전달

세션 → 로그인 상태 저장

request.getParameter(), request.setCharacterEncoding("utf-8") → 요청 데이터 수신 및 인코딩 설정

response.sendRedirect() → 페이지 이동(리다이렉트)

jsp:include → 공통 메뉴/부분 파일 포함

## JSP 시험 대비 핵심 코드 포인트
#### 1. 요청 파라미터 읽기 + 인코딩 설정
jsp
코드 복사
<%
    request.setCharacterEncoding("utf-8");
    String userId = request.getParameter("user_id");
    String password = request.getParameter("password");
%>
폼 데이터 받을 때 request.getParameter()

한글 인코딩 문제 방지 위해 request.setCharacterEncoding("utf-8") 필수

#### 2. 세션 사용 예
jsp
코드 복사
<%
    session.setAttribute("userId", userId);
    session.setAttribute("userName", userName);
%>
로그인 성공 시 세션에 사용자 정보 저장

세션 무효화(로그아웃)

jsp
코드 복사
<%
    session.invalidate();
%>
#### 3. 조건문으로 로그인 여부 체크 및 화면 분기
jsp
코드 복사
<%
    boolean isLogin = session.getAttribute("userId") != null;
%>

<% if (isLogin) { %>
    <p>로그인 사용자: <%= session.getAttribute("userName") %>님 환영합니다.</p>
<% } else { %>
    <p>로그인이 필요합니다.</p>
<% } %>
#### 4. 반복문으로 리스트 출력 (회원, 게시글 목록)
jsp
코드 복사
<%
    List<MemberDto> memberList = memberService.getMemberList();
    for (MemberDto member : memberList) {
%>
    <tr>
        <td><%= member.getUserId() %></td>
        <td><%= member.getUserName() %></td>
    </tr>
<% } %>
#### 5. 삭제 확인 후 처리 버튼
html
코드 복사
<button onclick="return confirm('삭제하시겠습니까?') ? location.href='member-delete.jsp?user_id=<%=member.getUserId()%>' : false;">
    삭제
</button>
자바스크립트 confirm() 으로 삭제 여부 확인 후 이동

#### 6. 폼 작성 및 전송
html
코드 복사
<form action="/member-add-submit.jsp" method="post">
    <input type="text" name="user_id" required/>
    <input type="password" name="password" required/>
    <button type="submit">회원 추가</button>
</form>
POST 방식으로 폼 데이터 전송

서버단 JSP에서 request.getParameter() 로 받음

#### 7. 페이지 리다이렉트
jsp
코드 복사
<script>
    location.href = 'member-list.jsp';
</script>
또는

jsp
코드 복사
<%
    response.sendRedirect("member-list.jsp");
%>
데이터 처리 후 목록 페이지 등으로 이동

#### 8. jsp:include 를 이용한 공통 메뉴/부분 파일 포함
jsp
코드 복사
<jsp:include page="include_menu.jsp"/>
재사용 가능한 메뉴, 헤더, 푸터 등을 포함할 때 사용

# 요약

| 기능               | 핵심 코드 예시                                   | 설명                          |
|------------------|---------------------------------------------|-----------------------------|
| 요청 데이터 받기      | `request.getParameter("name")`                 | 폼 데이터 받아오기                  |
| 한글 인코딩 설정      | `request.setCharacterEncoding("utf-8")`         | 한글 깨짐 방지                   |
| 세션 저장/읽기        | `session.setAttribute("key", value)` / `session.getAttribute("key")` | 로그인 상태 유지, 사용자 정보 저장 및 조회 |
| 세션 종료 (로그아웃)   | `session.invalidate()`                         | 세션 데이터 삭제 및 로그아웃 처리          |
| 조건문              | `<% if(condition) { %> ... <% } %>`            | 로그인 여부 등 조건 분기 처리           |
| 리스트 반복 출력      | `<% for(Type obj : list) { %> ... <% } %>`     | DB 조회 결과를 반복 출력             |
| 폼 작성 및 전송       | `<form action="submit.jsp" method="post">`     | 사용자 입력 폼 생성 및 서버 전송         |
| 삭제 확인 및 이동      | `onclick="return confirm('삭제?') ? location.href='delete.jsp?id=...' : false;"` | 삭제 전 사용자 확인 후 이동 처리         |
| 페이지 이동 (리다이렉트) | `response.sendRedirect("page.jsp");` 또는 `<script>location.href='page.jsp';</script>` | 처리 완료 후 다른 페이지로 이동           |
| JSP 파일 포함        | `<jsp:include page="include.jsp"/>`             | 공통 UI 파일 포함(메뉴, 헤더 등)         |
