# 목차
1. [Table](#Table)
2. [TaskListItems](#TaskListItems)
3. [Strikethrough](#Strikethrough)
4. [Autolinks](#Autolinks)
5. [DisallowedRawHTML](#DisallowedRawHTML)

___

# Table
> GFM enables the extension, where an additional leaf block type is available.
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
> - 


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
