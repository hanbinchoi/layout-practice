# Before Grid

grid가 나오기전에 flex로 테이블형태로 처리하기 위해서는 wrap 속성을 통해 처리가 가능하지만 불편한점이 많다.

element간에 가로와 세로 사이에 공간을 주기위해 justify-content, align-items 등 속성을 주고 처리하지만, 또 element가 들어오면 다시 속성을 주고 처리해야 한다.

> 혹은 여러개의 flex를 통해 테이블을 생성한다.

이처럼 grid 형태가 만들기 어려워 등장한게 grid이다.

---

# Grid

Grid도 flexbox처럼 부모로 부터 선언이 된다.

grid는 대부분 속성이 부모에 종속된다.

## grid-template-columns,rows

grid의 row와 column개수를 설정할 수 있다.

```css
grid-template-columns: 20px 55px 100px;
```

원하는 개수 크기를 입력한다.

이렇게 되면 element들은 자동으로 grid 크기만큼 설정되고, 4번쨰 element는 2번째 라인으로 가서 20px로 생성된다.

```css
grid-template-columns: 1fr 1fr 1fr;
```

fr은 컨테이너의 fraction을 의미한다.

fraction은 사용가능한 공간이다.

이렇게 grid의 공간에서 각 1/3씩 가져가게 된다.

pixel로 크기를 지정하지 않아 반응형 웹에 아주 적합하다.

## 오로지 차지할 공간만 숫자를 할당하면 브라우저의 컨테이너 크기에 맞게 자동으로 반환한다.

## column,row-gap

gap은 elemnt사이에 공간크기를 할당한다.

```css
column-gap: 10px;
```

10px로 설정되었으므로 element사이에 10px의 빈공간이 할당된다.

앞 서 column에 대해서만 예제를 적용했는데, 이때 row의 크기는 font-size에 종속된다.

row의 크기를 따로 설정하지 않았기 때문이다.

```css
grid-template-columns:
  repeat(4, 200px)
  auto; /* 200px, 200px, 200px, 200px;와 같음 */
```

> auto는 나머지 공간을 자동으로 채운다

---

## grid-template-areas

areas는 element의 이름을 설정하여 각 이름마다 크기를 할당해 줄 수 있다.

```css
.container {
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 20px 100px;
  grid-template-areas:
    "header header header"
    "content content content";
}

.header {
  grid-area: header;
}

.content {
  grid-area: content;
}
```

이렇게 class에는 변화를 주지않고 css에서 grid-area로 이름을 주고

부모인 container에서 각 area가 할당될 위치를 준다.

---

## grid-column-start, end

start는 자식에게 주는 속성으로 해당 element가 시작하는 열을 지정한다.

end는 element가 끝날 열을 지정한다.

start부터 end까지 element자체를 늘리는 것이다.

area는 element를 늘리는것이 아닌, 하나하나 그 자리에 배치되는 것이다.

```
grid-column-start: 1;
grid-column-end:  3;
```

이렇게 지정되면 해당 element는 첫번째 column부터 3번쨰 column까지 위치를 차지한다.

여기서 숫자는 라인을 의미한다.

라인은 element사이의 경계선을 의미한다.

이러한 start와 end는 row도 마찬가지로 적용되며

element의 위치를 grid안에서 자유롭게 지정할 수 있다.

---

## grid-template

```css
grid-template:
  "header header header header " 1fr
  "content content content nav" 2fr
  "footer footer footer footer" 1fr / 1fr 1fr 1fr 1fr;
```

grid-template는 처음에 area로 row를 적는다. 그리고 row의 높이를 정한다.

마지막줄 / 1fr 1fr 1fr 1fr은
컬럼의 길이를 설정하였다.

---

## grid-column

앞에 본 start, end를 생략하는 방법이다.

```css
grid-column: 1/5;
```

```css
grid-column-start: 1
gird-column-end: 5;
```

두 코드는 같은 역할이다.

line의 수를 직접 세는 것도 있지만

```css
grid-column: 1/-1;
```

이렇게 -1은 마지막 라인을 의미한다.

라인은 끝에서 -1, -2, -3으로 셀 수 있어, 마지막에서 첫번째, 두번쨰 라인을 논리적으로 지정가능하다.

span으로도 표현이 가능하다

```css
grid-column: span 4;
```

span은 4개의 cell을 가지라는 의미이다.

element가 총 4칸을 갖게 된다.

---

---

## justify-items

기본값은 stretch이다.

수평으로 동작한다.

즉, 컨테이너는 grid자식을 갖고 있고, 자식들을 늘여서 cell을 채운다.

**property**

- start: item을 늘이지 않고 처음부터 시작함.
- center: 중앙으로 item 정렬
- end: 마지막으로 정렬

---

## align-items

justify item이랑 비슷하다.

수직으로 동작한다.

align-items를 통해 cell 안에 수직으로 아이템을 배치한다.

start, end, center 등이 있다.

---

## place-items

place-items는 수평과 수직을 한번에 동작하게 하는 방법이다.

```css
place-items: stretch/center; //수직, 수평 순.
```

수직(align-items), 수평(justify-items) 순으로 적는다.

---

## justify-content

item은 각 cell을 의미한다.

content는 grid를 자체를 의미한다.

grid element는 100% width인데,
grid-content는 그 100% 넓이에서 grid 자체를 움직인다.

end, start, center, space-around 같은 속성이 사용 가능하다.

---

## align-content

justify는 column을 배치하는 방식이고,

align-content는 raw를 배치한다.

grid는 height는 100%가 아니라 크기를 지정해야한다.

그 지정한 크기에서 grid의 raw위치들이 지정되게 하는 속성이다.

**content는 grid자체를 움직이는 속성이다**

**item은 각 cell을 움직이는 속성이다**

---

## place-content

place-item같이 수직, 수평 순으로 써서 한번에 align, justify를 설정한다.

---

## align-self, justify-self, place-self

앞서 item, content는 컨테이너에 적용한 속성이다.

self는 자식에서 속성을 부여한다

각 cell 자체에 center, end, start등을 부여해 각 cell이 grid 안에서 각각 다르게 위치하도록 지정할 수 있다.

---

## grid-auto-rows

grid의 설정한 row \* column 보다 많은 element가 grid에 들어오면 초과된 element들은 지정한 크기로 들어오지 못한다.

```css
grid-template-columns: reapeat(4,100px);
grid-auto-rows; 100px;
```

grid-auto-rows는 만약 더 많은 content가 들어오면 row를 지정하지 않아도 디펄트 값을 자동으로줘서 크기를 지정한다.

이렇게 지정되면 4개의 컬럼으로 값이 저장되면서 데이터가 몇개나 들어올지 row로 적지 않아도 되어 효율적이다.

## grid-auto-flow

만약 새로운 row를 만들지않고 새로운 column을 하고싶다면

```css
grid-auto-flow: column;
grid-auto-columns: 100px;
```

를 한다.

또한 flex-direction같이 element가 들어가는 방향을 설정한다.

columns를 설정할 경우 element는 세로방향으로 쌓이게 된다.

---

## minmax

minmax는 element를 얼마나 크게, 작게 설정할 것이냐는 값이다.

```css
grid-template-columns: repeat(10, minmax(100px, 1fr));
```

이렇게 설정하면 클때는 1fr을 할당하지만, 작아져서 1fr이 100px보다 작아지면 크기는 100px로 설정되고, 창의 크기는 더이상 작아질 수 없게 만든다.

---

## auto-fill, auto-fit

auto-fill은 minmax에서 선언한 크기를 유지한다.

윈도우 크기가 커지면 새로운 컬럼이 생성되어 옆에 element가 배치되고 작아지면 컬럼이 제거되면서 element가 row로 이동한다. 그러다가 100px보다 작아지면 멈춘다.

auto-fit은 윈도우가 작아지면 같이 작아지다가 element가 row로 이동한다. 100px보다 작아지면
멈춘다.

윈도우 크기가 커지면 빈 컬럼이 들어오는 것이 아닌, cell자체가 늘어진다.

```css
grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));

grid-template-columns: repeat (auto-fit, minmax(100px, 1fr));
```

다시 정리하자면,

auto-fill은 창 너비가 늘어나면 빈 컬럼들로 row를 채우게 되고

auto-fit은 창 너비가 늘어나면 element를 늘려서 row에 맞게 채운다.

auto-fit은 유동적인 사이즈를 맞추고

auto-fill은 보다 정확한 사이즈를 맞춘다.

---

## min-content, max-content

max-content는 박스를 필요한 만큼 크게 만든다.

min-content는 박스를 작아질 수 있는 만큼 작아지게 만든다.

```css
grid-template-columns: max-content min-content;
```

max-content는
cell의 text크기가 매우 길면 text길이만큼 박스가 커진다.

min-content는 cell의 text크기가 매우 길때 text길이가 아닌 최대한 작아지게 만든다.

따라서 글씨가 꺠지거나 해도 상관안한다.

```css
grid-template-columns: repeat(5, minmax(max-content, 1fr));
```

이렇게 작성하면 컨텐츠의 길이만큼 크기가 자동으로 할당된다.
