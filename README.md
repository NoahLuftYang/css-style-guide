# Airbnb CSS / Sass 스타일 가이드

*CSS와 Sass에 대한 가장 합리적인 접근 방법*

## 목차

  1. [용어 설명](#용어-설명)
    - [규칙 선언부](#규칙-선언부)
    - [선택자](#선택자)
    - [속성](#속성)
  1. [CSS](#css)
    - [형식](#형식)
    - [주석](#주석)
    - [OOCSS와 BEM](#oocss와-bem)
    - [ID 선택자](#id-선택자)
    - [자바스크립트 후크](#자바스크립트-후크)
    - [Border](#border)
  1. [Sass](#sass)
    - [Syntax](#syntax)
    - [Ordering](#ordering-of-property-declarations)
    - [Variables](#variables)
    - [Mixins](#mixins)
    - [Extend directive](#extend-directive)
    - [Nested 선택자](#nested-선택자)
  1. [Translation](#translation)

## 용어 설명

### 규칙 선언부

"규칙 선언부(Rule declaration)"는 특정 속성 그룹을 따르는 선택자(또는 선택자로 묶인 그룹)에게 부여되는 이름입니다. 다음 예시를 참조해주세요:

```css
.listing {
  font-size: 18px;
  line-height: 1.2;
}
```

### 선택자

규칙 선언부에서, "선택자(Selectors)"는 DOM 트리의 어떤 요소들이 정의된 속성(Properties)으로 꾸며질지 결정하는 부분들입니다. 선택자는 HTML 요소들, 뿐만 아니라 한 요소의 클래스, ID, 또는 해당 요소의 어느 속성(attributes)들과도 연결될 수 있습니다. 다음은 선택자에 대한 예시들입니다:

```css
.my-element-class {
  /* ... */
}

[aria-hidden] {
  /* ... */
}
```

### 속성

마지막으로, "속성(Properties)"은 규칙 선언부의 선택된 요소들이 그들의 스타일을 가지게 하는 것입니다. 속성은 키-값의 쌍으로 구성되며, 규칙 선언부는 하나 이상의 속성 선언부를 가질 수 있습니다. 속성 선언부는 아래와 같은 형태입니다:

```css
/* 특정 선택자 */ {
  background: #f1f1f1;
  color: #333;
}
```

## CSS

### 형식

* 부드러운 탭(띄어쓰기 2칸) 들여쓰기를 사용하세요.
* 클래스 이름에는 camelCase 방식보다 대시(-)를 사용하세요.
  - 만약 당신이 BEM(아래 [OOCSS와 BEM](#oocss와-bem) 참조)을 사용하고 계신다면 밑줄(_)과 PalcalCase 방식을 사용하셔도 괜찮습니다.
* ID 선택자를 사용하지 마세요.
* 당신이 규칙 선언부에서 다중 선택자를 사용하실 때, 선택자를 한 줄에 한개씩 적어주세요.
* 규칙 선언부의 여는 괄호 `{` 이전에 띄어쓰기를 넣어주세요.
* 속성 부분에서, `:` 문자 뒤에 띄어쓰기를 넣어주세요. 단, `:` 문자 앞에는 띄어쓰기를 넣지 말아주세요.
* 규칙 선언부의 닫는 괄호 `}`를 새로운 줄에 넣어주세요.
* 규칙 선언부들 사이에 빈 줄을 넣어주세요.

**잘못된 예시**

```css
.avatar{
    border-radius:50%;
    border:2px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
```

**올바른 예시**

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```

### 주석

* 블록 형식 주석보다 라인 형태 주석(Sass일 경우 `//`)을 권장합니다.
* 주석을 새로운 줄에 적어주세요. 선택자 또는 속성과 같은 줄에 주석을 작성하는 방식을 피해주세요.
* 코드 자체만으로 이해하기 어려운 경우 자세한 주석을 작성해주세요:
  - z-index를 사용하는 경우
  - 특정 브라우저를 지원하기 위해 사용하는 경우

### OOCSS와 BEM

우리는 다음과 같은 이유로 OOCSS와 BEM의 혼용을 권장합니다:

  * CSS와 HTML 사이의 명확하고, 엄격한 관계를 형성하는 데에 도움을 줍니다
  * 재사용 가능하고, 작성 가능한 컴포넌트를 만드는 데에 도움을 줍니다
  * 보다 적은 중첩과 낮은 특수성을 갖게 합니다
  * 확장성 있는 스타일시트를 작성하도록 도움을 줍니다

**OOCSS**, 또는 “Object Oriented CSS”는 당신의 스타일시트를 "객체"의 모음(한 웹사이트에서 독립적으로 사용되는, 재사용 가능하고 반복 가능한 단편들)로 판단하게 만드는 CSS 작성을 위한 접근 방식입니다.

  * Nicole Sullivan의 [OOCSS wiki](https://github.com/stubbornella/oocss/wiki)
  * Smashing Magazine의 [Introduction to OOCSS](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/)

**BEM**, 또는 “Block-Element-Modifier”는 HTML과 CSS 내부의 클래스에 대한 _명명 협약_입니다. 이것은 원래 대량의 코드베이스와 확장 가능성을 염두해두고 Yandex에서 개발되었으며, OOCSS 구현을 위한 견고한 가이드라인으로 사용될 수 있습니다.

  * CSS Trick의 [BEM 101](https://css-tricks.com/bem-101/)
  * Harry Roberts의 [introduction to BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)

우리는 React와 같은 컴포넌트들과 결합할 때 부분적으로 잘 작동하는 PascalCase 형태의 "블록들"과 함께 BEM의 변형을 권장합니다. 밑줄과 대시는 아직 변형자와 자식에게 사용됩니다.

**예시**

```jsx
// ListingCard.jsx
function ListingCard() {
  return (
    <article class="ListingCard ListingCard--featured">

      <h1 class="ListingCard__title">Adorable 2BR in the sunny Mission</h1>

      <div class="ListingCard__content">
        <p>Vestibulum id ligula porta felis euismod semper.</p>
      </div>

    </article>
  );
}
```

```css
/* ListingCard.css */
.ListingCard { }
.ListingCard--featured { }
.ListingCard__title { }
.ListingCard__content { }
```

  * `.ListingCard` is the “block” and represents the higher-level component
  * `.ListingCard__title` is an “element” and represents a descendant of `.ListingCard` that helps compose the block as a whole.
  * `.ListingCard--featured` is a “modifier” and represents a different state or variation on the `.ListingCard` block.

### ID 선택자

While it is possible to select elements by ID in CSS, it should generally be considered an anti-pattern. ID 선택자 introduce an unnecessarily high level of [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) to your 규칙 선언부s, and they are not reusable.

For more on this subject, read [CSS Wizardry's article](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) on dealing with specificity.

### JavaScript hooks

Avoid binding to the same class in both your CSS and JavaScript. Conflating the two often leads to, at a minimum, time wasted during refactoring when a developer must cross-reference each class they are changing, and at its worst, developers being afraid to make changes for fear of breaking functionality.

We recommend creating JavaScript-specific classes to bind to, prefixed with `.js-`:

```html
<button class="btn btn-primary js-request-to-book">Request to Book</button>
```

### Border

Use `0` instead of `none` to specify that a style has no border.

**Bad**

```css
.foo {
  border: none;
}
```

**Good**

```css
.foo {
  border: 0;
}
```

## Sass

### Syntax

* Use the `.scss` syntax, never the original `.sass` syntax
* Order your regular CSS and `@include` declarations logically (see below)

### Ordering of property declarations

1. Property declarations

    List all standard property declarations, anything that isn't an `@include` or a nested selector.

    ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      // ...
    }
    ```

2. `@include` declarations

    Grouping `@include`s at the end makes it easier to read the entire selector.

    ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);
      // ...
    }
    ```

3. Nested 선택자

    Nested 선택자, _if necessary_, go last, and nothing goes after them. Add whitespace between your 규칙 선언부s and nested 선택자, as well as between adjacent nested 선택자. Apply the same guidelines as above to your nested 선택자.

    ```scss
    .btn {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);

      .icon {
        margin-right: 10px;
      }
    }
    ```

### Variables

Prefer dash-cased variable names (e.g. `$my-variable`) over camelCased or snake_cased variable names. It is acceptable to prefix variable names that are intended to be used only within the same file with an underscore (e.g. `$_my-variable`).

### Mixins

Mixins should be used to DRY up your code, add clarity, or abstract complexity--in much the same way as well-named functions. Mixins that accept no arguments can be useful for this, but note that if you are not compressing your payload (e.g. gzip), this may contribute to unnecessary code duplication in the resulting styles.

### Extend directive

`@extend` should be avoided because it has unintuitive and potentially dangerous behavior, especially when used with nested 선택자. Even extending top-level placeholder 선택자 can cause problems if the order of 선택자 ends up changing later (e.g. if they are in other files and the order the files are loaded shifts). Gzipping should handle most of the savings you would have gained by using `@extend`, and you can DRY up your stylesheets nicely with mixins.

### Nested 선택자

**Do not nest 선택자 more than three levels deep!**

```scss
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```

When 선택자 become this long, you're likely writing CSS that is:

* Strongly coupled to the HTML (fragile) *—OR—*
* Overly specific (powerful) *—OR—*
* Not reusable


Again: **never nest ID 선택자!**

If you must use an ID selector in the first place (and you should really try not to), they should never be nested. If you find yourself doing this, you need to revisit your markup, or figure out why such strong specificity is needed. If you are writing well formed HTML and CSS, you should **never** need to do this.

## Translation

  This style guide is also available in other languages:

  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [Zhangjd/css-style-guide](https://github.com/Zhangjd/css-style-guide)
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**: [Nekorsis/css-style-guide](https://github.com/Nekorsis/css-style-guide)
  - ![ja](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [nao215/css-style-guide](https://github.com/nao215/css-style-guide)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [ismamz/guia-de-estilo-css](https://github.com/ismamz/guia-de-estilo-css)
  - ![PT-BR](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Portuguese**: [felipevolpatto/css-style-guide](https://github.com/felipevolpatto/css-style-guide)
