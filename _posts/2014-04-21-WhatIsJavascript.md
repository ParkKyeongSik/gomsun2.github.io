---
layout: post
title:  "자바스크립트란 무었인가"
date:   2014-04-21 18:11:00
categories: javascript
---

# 자바스크립트란 무었인가 ?

**by gomsun2**

[toc]

Javascript는 서버에서 수행되었던 유효성검사를 클라이언트에서 수행하기위하여 고안되었다.

이 후 점차 발전하여 Web Browser의 창(Window)과 거의 모든 Contents와 상호 작용을 하게 된다.

## 구성

- ECMA Script
- DOC(Document Object Model)
- BOM(Browser Object Model)
![JavacriptStack](https://github.com/gomsun2/gomsun2.github.io/_posts/2014-04-21-jsStructure.png)

## ECMA Script

### Javascript는 호스트 환경을 필요로 한다

예를 들어 Browser라는 호스트 환경은

- ECMA Script 구현
- DOM 환경

을 제공한다.

다른 호스트 환경으로는 Node.js, Adobe Flas(Action Script)등이 있다.

### ECMA Script 표준 준수

- 항상만족
  - 형(Type)과 값(Value), Object, Prototype, Function, 문법, 시멘틱을 ECMA-262에 표기한대로 구현한다.
  - 유니코드 표준을 지원
- 선택사항
  - ECMA-262에 정의하지 않은 Type, Value, Object, Property, Function을 추가 할 수 있으며, 새로운 Object나 Property로 간주한다.
  - 내장된 정규표현식을 확장할 수 있다.(이는 ECMA-262에 정의되지 않은 Program이나 정규표현식 문법 지원이 가능함을 이야기 한다.)


## DOM(Document Object Model)

- XML(eXtensible Markup Language)을 HTML에서 사용할 수 있도록 확장한 API이다.
- DOM은 전체 Page를 Node계층 구조(Tree)로 반환한다.
  -
```HTML
<body>
	<table>
		<tr>
			<td>value</td>
		</tr>
	</table>
 </body>
```
![JavacriptStack](https://github.com/gomsun2/gomsun2.github.io/_posts/2014-04-21-DOMTree.png)
- 개발자는 DOM API를 통해 문서구조, CONTENTS를 추가, 수정, 삭제, 생성 할 수 있다.

### DOM Level

#### DOM Level 1

- DOM Core: Node 접근, 조작
- DOM HTML
  - DOM Core의 확장
  - HTML에 밀접한 객체와 메소드를 제공

#### DOM Level 2

- DOM Core: NameSpace 제공
- DOM View: 문서의 다양한 뷰를 제공.
  - 예를 들어, CSS 적용 전/후를 추적하는 Interface를 제공한다.
- DOM Event: Event, Event Handler에 관한 Interface를 제공
- DOM Style: CSS를 통해 요소의 스타일을 바꾸는 Interface를 제공
- DOM Model & Scopte: 문서 Tree를 이동/조작하는 Interface를 제공

#### DOM Level 3

- DOM의 확장
- 문서 저장, 불러오기의 (호스트환경 간)통일된 방법 제공
- 문서 유효성 검사
- DOM Core: XML Infoset, XPath, XML Base를 포함하는 XML 1.0 지원

## BOM(Browser Object Model)

- Browser 창의 접근/ 조작 Interface 제공
- HTML 5부터 표준으로 제정
