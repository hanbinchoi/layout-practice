# SCSS

SCSS는 CSS를 preprocessing하는 syntax이다.

CSS를 programming language처럼 만들어서 변수, 확장 등을 사용할 수 있다.

programming language이기 때문에 compile과 build의 과정이 필요하다.

conolse에서 error메세지를 출력하기 때문에 빠른 오류수정이 가능하다.

---

## Variable

scss에서 변수를 생성하는 방법은

src폴더에 \_로 시작하는 scss파일을 만들고 그 파일안에

```scss
$name: value;
```

이다.

그리고 그 파일을 사용하기 위해

```scss
@import "file name";

body {
  background-color: $name;
}
```

해준다

---

## Nesting

Nesting은 타겟하는 element를 정확하게 해준다.

만약 box의 자식 타겟을 명확하게 하려면

```scss
.box {
  h2 {
    ...
  }
  button {

  }
  &:hover { //.box: hover와 같다.

  }
}
```

이렇게 box안에 element만 지정이 가능하다.

이렇게 모든 box안에 element를 표현가능해서 좀 더 코드가 간소화 된다.

---

## mixins

mixins는 \_ scss파일에 @minix으로 선언하여 사용한다.

```scss
@mixin title {
  color: blue;
  font-size: 20px;
}
```

그 후 styles.scss파일에서

```scss
@import "_mixins";

h1 {
  @include title();
}
```

h1태그는 title함수에 작성된 스타일로 적용된다.

이렇게 mixin은 함수처럼 작용한다.

```scss
@mixin link($color) {
  text-decoration: none;
  display: block;
  color: $color;
}

a {
  margin-bottom: 10px;

  &:nth-child(odd) {
    @include link(blue);
  }

  &:nth-child(even) {
    @include link(red);
  }
}
```

이렇게 mixins 함수에 파라미터 변수를 넘겨 각각 다르게 동작하도록 조작할 수 있다.

```scss
@mixin link($word) {
  @if $word == "odd" {
    color: red;
  } @else {
    color: blue;
  }
}
```

일반 프르그램 언어에서 사용하는 if-else문도 사용가능하다.

mixin은 argument에 따라 css의 결과값을 받게할 때 유용하다.

---

## Extends

Extends는 같은 코드를 중복해서 사용하지 않도록 해준다.

이미 작성된 코드를 다시 작성할 필요없이 extends를 통해 불러온다.

```scss
//styles.scss
@import "_buttons";

a {
  @extend %button;
  color: blue;
}

button {
  @extend %button;
}

// ---------

//_buttons.scss

%button {
  border-radius: 7px;
  font-size: 12px;
  text-transform: uppercase;
  padding: 5px 10px;
}
```

이렇게 중복된 스타일은 그냥 extend를 통해 변수를 불러와서 사용하고 추가적인 부분만 따로 코딩해준다.

---

## SCSS 라이브러리 사이트

### [Bourbon](https://www.bourbon.io/) <- color, magin, border, etc ...

### [Animate.scss](https://animate.style/) <- Animation

### [another](https://github.com/colourgarden/awesome-scss) <- All the SCSS
