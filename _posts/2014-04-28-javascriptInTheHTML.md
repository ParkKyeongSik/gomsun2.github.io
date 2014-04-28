---
layout: post
title:  "2장 HTML속의 javascript"
date:   2014-04-28 18:20:00
categories: javascript
---

# 2장 HTML속의 javascript

by gomsun2

## `<Script>`란

HTML 페이지에 `<script>`요소를 통해 javascript를 삽입할 수 있습니다.

### `<script>`속성

- src: javascript code가 작성된 file 위치를 명시
- type
  - script언어의 MIME type을 명시하는 용도
  - `type="text/javascript"`와 같이 작성합ㄴ디ㅏ.
  - 만일, `type`속성을 생략하면 Browser는 `type="text/javascript"`를 기본 값으로 인식합니다.
- defer
  - **사용하지 말것**
  - `defer` 명시 순차적으로 js파일을 내려 받은 후 나중에 평가 한다.
- async
  - **사용하지 말것**
  - 비동기 적으로 저장하고 비동기 적으로 평가한다.
- language / charset: **사용하지 말자**

### `<script>` 요소의 실행

- browser는 순차적으로 html 문서를 읽고 redering 중
- src 속성이나 inline 형태로 작성된 `<script>`요소를 만나면
  - intepreter가 순차적으로 해석
  - intepreter에 **`<script>`요소를 저장**
  - intepreter가 **평가**
- 해당 작업이 끝낸 후 html문서의 해석을 마지막 읽은 위치에서 작업을 재개한다.

### inline javascript

- `<script>`요소로 html 문서에 정의된 js code
- 만일 `<script>`요소에 `src`와 js code가 혼재 한다면
  - inline code는 무시하고, browser는 오류를 알린다.
  - html5 부터는 js의 주석 `//`만을 작성 할 수 있다.

### inline javascript의 위치

- 통상적으로 `<body>`요소의 마지막에 위치 한다.
- `<head>`요소에 위치 한다면...
  - 이는 html 문서에 필요한 js, css와 같은 형태의 요소를 한곳에 두고, 관리의 편리를 취하기위한 관례이다.
  - `<head>`요소에서 해석, 저장, 평가 후 `<body>`요소가 redering 된다.
  - 때문에 js 양 만큼 html 문서의 redering이 지연된다.

## XHTML(eXtensible Hyper Text Markup Language)과 lagecy brawser

- 구문 규칙상 XHTML에 포함된 `<script>`요소를 inline code로 구성하면 `<`와 같은 javascript 문법이 정상적으로 해석되지 않는다.
  - XHTML은 `<>`요소가 `</>`사이에 `<`가 온다면 오류로 취급함.
- 일부 mosaic / lagecy brawser는 javascript를 지원하지 않아 inline 코드가 오류를 발생 시킬 수 있다.
- 때문에 다음과 같은 2가지 해결책이 제시된다.
  - `src`속성으로 js를 다룬다.
  - HTML과 javascript의 주석을 조합하여 browser를 속인다.

```js
<script type="text\javascript"><!--
//<!CDATA[

//]]>
//-->
</script>
```

## 문서모드

js의 흑역사시절 비표준 기능 지원을 위해 IE에서 도입, 향후 다른 brawser도 지원하기 시작한다.

`<!DOCTYPE>` 요소를 정의하여 문서모드를 구분한다.

- 퀵모드: `<!DOCTYPE>` 요소가 정의되지 않으면 퀵모드
- 표준모드: 아래 두개 항목을 통칭 "표준모드"라고 한다. `<!DOCTYPE>` 요소로 구분한다.
	- 표준모드: see - http://htmlcss.kr/html/basic/doctype/
    - `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">`
    - `<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">`
	- 거의 표준모드

## `<noscript>` 요소

brawser가 js를 지원하지 않을 경우 `<noscript>` 요소가 실행된다.
