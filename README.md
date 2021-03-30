# GFM's Extended Syntax

___

# 목차
1. [Table](#Table)
2. [TaskListItems](#TaskListItems)
3. [Strikethrough](#Strikethrough)
4. [Autolinks](#Autolinks)
5. [DisallowedRawHTML](#DisallowedRawHTML)

___

# Table
> GFM enables the extension, where an additional leaf block type is available.
> 
> - Table은 행과 열로 있는 데이터 배열로, 단일 헤더 행, 데이터에서 헤더를 분리하는 delimiter 행 및 0개 이상의 데이터 행으로 구성됩니다.
  
> - 각 행은 파이프( | )로 구분되는 인라인 구문과 임의 텍스트가 포함된 셀로 구성됩니다. 선행 및 후행 파이프는 읽기의 명확성을 위해 권장되며, 그렇지 않은 경우 구문 분석에 있어 모호성이 있을 수 있습니다. 파이프와 셀 콘텐츠 사이의 공백이 잘리고 블록 수준 요소는 테이블에 삽입할 수 없습니다.

> - The delimiter 행은 유일한 함량이 하이픈(|) 및 선택적으로 선행 또는 후행 결장 또는 둘 다인 셀로 구성되어 각각 왼쪽, 오른쪽 또는 중앙 정렬을 나타냅니다.

**example**  
```
ex 1)
  |foo|bar|
  |---|---|
  |baz|bim|
  
ex 2)
  |abc|defghi|
  :-:|--------:
  bar|baz

* 한 열의 셀은 길이를 일치할 필요는 없지만, 이 열의 경우 읽기가 더 쉽습니다. 또한, 선행 및 후행 파이프의 사용이 일치하지 않은 수 있습니다.

ex 3)
  |f\|oo |
  |-----|
  |b `\|` az |
  |b **\|** im |
  
* 다른 인라인 범위 내부를 포함하여 셀의 내용에 파이프를 포함합니다.

ex 4)
  |abc|def|
  |---|
  |bar|
  
* 헤더 행은 셀 수의 delimiter 행과 일치해야 합니다. 그렇지 않으면 테이블은 인식되지 않습니다.

ex 5)
  |abc|def|
  |---|---|
  |bar|
  |bar|baz|boo|
  
* 테이블행의 나머지 행은 셀 수에 따라 다를 수 있습니다.  
* 헤더 행의 셀 수보다 적은 셀이 여러 개 있는 경우 빈 셀이 삽입됩니다. 더 큰 경우는 무시됩니다.

ex 6)
  |abc|def|
  |---|---|

* 본문에 행이 없는 경우 HTML 출력에서 생성되지 않습니다.
```

<br>

___

# TaskListItems
> GFM을 사용하면 목록 항목에서 추가 처리 단계가 수행되는 확장을 사용할 수 있습니다.
> 
> - Task list items은 첫 번째 블록이 Task list items marker로 시작하는 단락이고 다른 내용보다 공백 문자가 하나 이상 있는 목록 항목입니다.
> - Task list items marker는 공백 수(선택 사항), 왼쪽 괄호(), 공백 문자 또는 소문자 또는 대문자, 오른쪽 괄호()로 구성됩니다.
> - 렌더링 시 Task list items marker는 의미 확인란 요소로 대체되며, HTML 출력에서 이것은 요소가 됩니다.
> 
> - 이 규격은 체크박스 요소가 상호 작용하는 방식을 정의하지 않습니다. 실제로 구현자는 확인란을 비활성화 또는 불변 요소로 자유롭게 렌더링하거나 최종 렌더링된 문서에서 동적 상호 작용(체크, 선택 해제)을 동적으로 처리할 수 있습니다.

**example**  
```
ex 1)
  - [ ] foo
  - [x] bar

ex 2)
  - [x] foo
    - [ ] bar
    - [x] baz
  - [ ] bin

* 작업 목록은 임의로 중첩될 수 있습니다.
```

<br>

___

# Strikethrough
> GFM을 사용하면 추가 강조 유형을 사용할 수 있는 확장을 사용할 수 있습니다.

**example**  
```
  ex 1)
    ~~Hi~~Hello, ssu!
  
  * Strikethrough 텍스트는 2 개의 '~'로 묶인 텍스트입니다.
  
  ex 2)
    This ~~has a
    
    new paragraph~~
  
  * 일반 강조 기호와 마찬가지로, 새로운 단락은 구문 분석을 통한 Strikethrough을 중단할 수 있습니다.
```

<br>

___

# Autolinks
> GFM을 사용하면 더 많은 조건에서 자동 링크가 인식되는 확장을 지원합니다.
>
> - 자동 링크는 더 작은 환경에서 인식될지라도 자동 링크를 사용하거나 구분하지 않고도 구성할 수 있습니다.
> - 확장된 www Autolink는 텍스트가 발견되고 유효한 도메인이 검색되면 인식됩니다.
> - 유효한 도메인은 영숫자, 밑줄 및 하이픈으로 구분된 세그먼트로 구성됩니다.
> - 기간이 하나 이상 있어야 하며 도메인의 마지막 두 세그먼트에 밑줄이 없을 수 있습니다

**example**  
```
1. Http
  ex 1)
     www.naver.com
  * http는 자동으로 삽입됩니다.
  
  ex 2)
    Visit www.naver.com/help for more information.
  * 유효한 도메인 이후에 공백이 없는 문자가 0개 이상 따를 수 있습니다.
```
> - Extended autolink path validation
>   1) 후행 문장 부호(특히 ,)는 링크의 내부에 포함 될 수 있지만, 자동 링크의 일부로 간주되지 않습니다.
>   2) 자동 링크가 끝나면 전체 자동 링크를 검사하여 총 괄호 수를 검사합니다.
>     - 닫는 괄호가 여는 괄호보다 많을 경우 자동 링크에서 일치하지 않는 괄호 부분은 고려하지 않습니다.
>     - 링크가 닫는 괄호에서 끝날 때만 수행되므로 내부에만 괄호가 있는 경우 특별한 규칙이 적용되지 않습니다.
>   3) 자동 링크가 세미콜론에서 끝나는 경우 entity reference와 유사한 것으로 보이는지 확인합니다.
>      - 앞 텍스트 다음에 하나 이상의 문자가 있으면 자동 링크에서 제외됩니다.
>   4) 자동 링크 종료됩니다.
    
    ※ entity reference : 유효한 HTML5 엔터티 이름 +로 구성됩니다.  
    https://html.spec.whatwg.org/multipage/entities.json 문서는 유효한 엔터티 참조와 해당 코드 포인트에 대한 권한 있는 소스로 사용됩니다. 


> - Extended url autolink : schemes나 유효한 도메인 다음에 확장된 자동 링크 경로 유효성 검사에 따라 0개의 공간과 문자가 없을 경우 인식됩니다.

2. Email
  - 모든 텍스트 노드 내에 전자 메일 주소를 인식할 때 확장된 전자 메일 자동 링크가 인식됩니다.  
  - 다음 규칙에 따라 인식됩니다.
      1) 영숫자 또는 , , , 또는 하나 이상의 문자입니다.(-_+)
      2) 기호(@)
      3) 영어, 숫자 또는 마침표로 구분된 하나 이상의 문자입니다. 마지막 문자는 '-_.-_' 중 하나일 수 밖에 없습니다.
```
  ex 1)
     foo@bar.baz
     
  * scheme가 생성된 링크에 자동으로 추가됩니다.
  
  ex 2)
     hello@mail+xyz.example isn't valid, but
     hello+xyz@mail.example is.
  
  * 앞에서는 발생할 수 있지만, 뒤에서는 발생할 수는 없습니다.

  ex 3)
     a.b-c_d@a.b
     a.b-c_d@a.b.
     a.b-c_d@a.b-
     a.b-c_d@a.b_
     
  * '.', ','의 양쪽에서 발생할 수 있지만, 이메일 주소의 끝에만 발생할 수 있습니다.
  * 이 경우 이메일 주소는 주소의 일부로 간주되지 않습니다.
```

<br>

___

# DisallowedRawHTML
> GFM을 사용하면 HTML 출력을 렌더링할 때 다음 HTML 태그가 필터링되는 확장을 사용할 수 있습니다.
> - <title>
> - <textarea>
> - <style>
> - <xmp>
> - <iframe>
> - <noembed>
> - <noframes>
> - <script>
> - <plaintext>
> 
> * 필터링은 선행을 엔터티로 대체하여 수행됩니다. 이러한 태그는 특히 HTML이 고유한 방식으로 해석되는 방식을 변경할 때 선택되며 일반적으로 렌더링 된 다른 Markdown 콘텐츠의 컨텍스트에서 신뢰할 수 없습니다.
> * 다른 모든 HTML 태그는 그대로 유지됩니다.

**example**  
```
  ex 1) 
    <strong><title><style><em>
      
     <blockquote>
        <xmp> is disallowed. <XMP> is a also disallowed
     </blockquote>
```
