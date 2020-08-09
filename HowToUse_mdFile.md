# How to use

[1. 줄바꿈이 안 될때](#1-줄바꿈이-안-될때)  
[2. 문서내 링크 (목차로 활용)](#2-문서내-링크-목차로-활용)  
[3. 글머리](#3-글머리)  
[4. 이미지 삽입](#4-이미지-삽입)  
[5. 표 만들기](#5-표-만들기)  
[6. 취소선 넣기](#6-취소선-넣기)  
[7. 주석 달기](#7-주석-달기)

## 1. 줄바꿈이 안 될때  
>일반 표현식은 자동으로 줄바꿈이 안 되는 경우가 있는데 줄의 끝에 스페이스 바 두 번 입력하고 줄 바꿈을 하면 한 줄 띄울 수 있다.  
예시: 목차를 만드는 경우, 줄 바꿈이 안 될수 있음  
해결: 스페이스바 두 번 + Enter

<br>

---

## 2. 문서내 링크 (목차로 활용)
>사용법 : `[링크명](#찾아갈목차명)`

>사용예시 :  
>[1. 옳은 Link 사용 (Table)](#1-옳은-link-사용-table)  
>[2. 틀린 Link 사용 (Table)](#2.-틀린-Link-사용-(Table))
>
>   
>
><br>
>
><br>
>
><br>
>
><br>

>#### 1. 옳은 Link 사용 (Table) 
>- `[1. 옳은 Link 사용 (Table)](#1-옳은-link-사용-table)`
>- 조건1: '찾아갈목차명'은 한글 또는 영어 소문자 그리고 숫자만 사용가능
>- 조건2: '찾아갈목차명' 내의 스페이스는 `-` 로 대신 입력
>- 조건3: 점, 콤마, 특수문자, 괄호 등은 무시
>- 조건5: `#` 또는 `###`등으로 제목처리된 곳으로만 링크 가능

>#### 2. 틀린 Link 사용 (Table)
>- 링크가 되지 않는 잘못된 사용의 경우  
>- `[2. 틀린 Link 사용 (Table)](#2.-틀린-Link-사용-(Table))` (틀린 경우)

<br>

---

# Table of Contents
1. [Example](#example)
2. [Example2](#example2)
3. [Third Example](#third-example)

## Example
## Example2
## Third Example

<br>

---

# Table of contents
1. [Introduction](#introduction)
2. [Some paragraph](#paragraph1)
    1. [Sub paragraph](#subparagraph1)
3. [Another paragraph](#paragraph2)

## 1. This is the introduction <a id="introduction"></a>
>Some introduction text, formatted in heading 2 style  
링크하는곳 : `[Introduction](#introduction)`  
링크받는곳 : `## 1. This is the introduction <a id="introduction"></a>`

## 2. Some paragraph <a id="paragraph1"></a>
>The first paragraph text
링크하는곳 : `[Some paragraph](#paragraph1)`  
링크받는곳 : `##2. Some paragraph <a id="paragraph1"></a>`

### 2-1.Sub paragraph <a id="subparagraph1"></a>
>This is a sub paragraph, formatted in heading 3 style
>* 링크하는곳 : `[Sub paragraph](#subparagraph1)`
>* 링크받는곳 : `### 2-1.Sub paragraph <a id="subparagraph1"></a>`

## 3. Another paragraph <a id="paragraph2"></a>
>The second paragraph text
링크하는곳 : `[Another paragraph](#paragraph2)`  
링크받는곳 : `## 3. Another paragraph <a id="paragraph2"></a>`

<br>

---

# Table of Contents (확인요망)
1. [Example](#example)
2. [Example2](#example2)
3. [Third Example](#third-example)

## Example [](#){name=example}
## Example2 [](#){name=example2}
## [Third Example](#){name=third-example}

<br>

---
## 3. 글머리

>사용방법: -, +, * 중 하나를 입력후 띄어쓰기 한번 하고 내용기입
>글머리 아래 글머리: 탭을 치고 아래 글머리 작성

### 글머리 목록
* Python
    * django
* Java
* Ruby
### 숫자 글머리
1. Python
    1. django
2. Java
3. Ruby


* Generate table of contents for Markdown files.
  Supported Markdown parsers:

  - [x] GFM (GitHub Flavored Markdown)
  - [x] GitLab
  - [x] Redcarpet

<br>

---
## 4. 이미지 삽입
* 이미지 삽입 방법: `![이미지 이름](이미지 URL)`
* ex) `![cat_image](img/cat.gif)`
![cat_image](img/cat.gif)

<br>

---
## 5. 표 만들기

|제목1|제목2|제목3|
|----|----|----|
| A | B | C |
|aa|bb|cc|
|xxx|yyy|zzz|

<br>

---

## 6. 취소선 넣기

예시) `여기에 ~~취소선~~을 넣습니다.`  
결과) 여기에 ~~취소선~~을 넣습니다.  

<br>

---

## 7. 주석 달기

마크다운(Markdown)은 일반 텍스트 문서의 양식을 편집하는 문법
이다.<sup>[1](#footnote_1)</sup> README 파일이나 온라인 문서, 혹은 일반 텍스트 편집기로
문서 양식을 편집할 때 쓰인다. 마크다운을 이용해 작성된 문서는
쉽게 HTML 등 다른 문서형태로 변환이 가능하다.<sup>[2](#footnote_2)</sup>

<br><br><br><br><br><br><br><br><br><br>
---
<a name="footnote_1">1</a>: 마크다운은 의외로 재미있고 마구 활용하고 싶어지는 규칙입니다.  
<a name="footnote_2">2</a>: [위키백과 마크다운 문서](http://ko.wikipedia.org/wiki/마크다운)