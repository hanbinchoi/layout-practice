# before flexbox

## block

블록은 element이고, 블록 옆에는 어떠한 element도 올 수 없다.

블록은 box이다.

즉, 블록의 기본속성은 윈도우 오른쪽으로 큰 마진이 생성된다.

## inline-block

인라인블록은 block의 속성을 유지하지만, 오른쪽 으로 쭉 펼쳐지는 마진을 없애서 옆에 다른 element가 올 수 있게된다.

## inline

인라인은 넓이와 높이를 쓸 수 없다. box속성이 아니며 옆으로 element가 배치된다.

---

#### 하지만 이러한 css속성들은 pixel로 값을 지정하여 반응형 웹에 적절히 대응하지 못한다.

---

# flexbox

flexbox 컨테이너를 사용하면 element 배치가 훨씬 간편하다.

```css
body {
  display: flex;
}
```

flexbox는 이처럼 컨테이너를 만들어 element를 컨테이너 안에 삽입한다.

여기서 주의할 점은 flex인 부모의 자식만 해당한다는 것이다.

flex의 자식의 자식들은 flex의 규칙에서 벗어난다.

flex에는 row와 column으로 컨테이너가 구성되어 있다.

flex-direction은 기본값이 row이다.

flex-direction:row 이면 가로축이 main axis가 된다.

값이 가로로 정렬된다는 것이다.

cross axis는 세로축이 된다.

row-reverse, column-reverse 처럼 거꾸로 element를 배치하는것도 존재한다.

---

justify-content는 main axis 방향으로 element를 옮긴다.

position 속성 중 하나인 justify-content는 main axis를 기준으로 center값을 주면 element는 중앙으로 정렬된다.

브라우저가 resize되도 flexbox가 자동으로 간격을 조절한다.

```css
justify-content: center;
```

**justify-content 속성**

- space between: box사이에 공간을 준다. (처음 과 마지막 element는 공간이 없음)
- space-around: box주변 옆 공간을 같게 만든다.

---

align-item은 element를 cross axis로 옮긴다.

center는 flexbox의 컨테이너 높이를 기준으로 가운데로 element를 옮긴다.

**align-item 속성**

- stretch: 전체 높이까지 채워짐
- flex-end: box의 맨끝에 item을 배치
- flex-start: box의 맨앞에 item을 배치

---

align-self는 align-item과 비슷하게 행동하지만 해당 자식만 유일하게 속성을 주는것이다.

해당 자식만 cross axis로 위치를 옮길 수 있다.

> align 속성은 부모의 높이가 지정되어야 정상적으로 동작한다.

> 만약 높이가 지정되지 않다면 cross axis의 범위가 없기 때문이다.

---

또다른 자식에게 줄 수 있는 속성은 order이다.

order:1; 로 속성을 주면 해당 자식은 부모 컨테이너의 두번째의 인덱스를 가진다.

box의 order는 0부터 시작한다.

하나의 박스만 order를 주면 나머지 박스는 기본적으로 0으로 설정되어 있으므로 맨 끝으로 이동한다.

---

> child에게 줄 수 있는 속성은 align-self와 order가 유일하다.

---

flexbox는 모든 element가 같은 라인(main axis)에 있도록 위치시킨다.

따라서 자식들의 크기는 flexbox에 의해 자동으로 변경된다.

flex-wrap이라는 속성은 nowrap이 기본값이다.

이 속성때문에 모든 element가 같은 라인에 위치하는 것이다.

만약 wrap이라는 값을 주면 같은 라인을 고집하지 않고 자식들의 크기를 유지하여 여러개의 라인이 생기게 된다.

wrap-reverse는 여러라인을 만드는데 element들이 반대순서로 배치된다.

---

align-content는 line을 수정할때 라인의 간격이 벌어지게 되는데 그것을 조정하는 속성이다.

align-content: flex-start; 는 라인시작의 간격을 없앤다.

center는 모든 라인이 가운데로 모인다.

space-between, space-around등이 사용이 가능하다.

justify-content는 element를 정의하는 것이고

align-content는 line을 정의하는 것이다.

---

flex-shrink는 기본적으로 element의 행동을 정의한다.

1이 기본값이다.

만약 값을 2로 변경하면 윈도우 크기가 줄어들때 shrink를 2로 준 element만 2배로 줄어든다.

flex-grow는 shrink와 반대로 동작한다.

값을 준 만큼 크기가 다른 element에 비해 커진다.

flex-grow의 기본값은 0이다.

만약 차지할 공간이 있으면 grow의 크기에 따라 element들이 가져간다.

여분공간이 없으면 할당된 공간은 같다.

> 이러한 속성들은 반응형 디자인에 유용하다

---
