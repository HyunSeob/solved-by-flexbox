---
template: default.html
title: 더 나은, 간단한 그리드 시스템
excerpt: Flexbox는 그리드 시스템에 필요한 대부분의 기능을 제공합니다. 사이즈 조절 및 정렬은 그냥 수 많은 속성 중 하나에 불과합니다.
---

대부분의 그리드 시스템은 `float` 혹은 `inline-block` 레이아웃 방식을 사용합니다. 하지만 이 방법들은 모두 실제로 레이아웃을 위해 사용되도록 의도된 방법이 아닙니다. 그 결과로, 꽤 중요한 문제와 한계를 가집니다.

float는 많은 레이아웃 문제를 가지고 있기 때문에 클리어(clear)하는 것이 요구됩니다. 가장 악명높은 문제는 요소를 클리어 했을 때 가끔 페이지 내 상관없는 부분 아래로 강제로 이동되는 것입니다. (예를 들어, 이 [Bootstrap issue](https://github.com/twbs/bootstrap/issues/295#issuecomment-2282969)를 참고하세요.) 게다가, float된 요소를 클리어하는 것은 대개 앞 뒤로 가상 요소(pseudo-element)를 필요로 하며, 이는 다른 용도로 사용할 수 없습니다.

Inline block 레이아웃은 [inline-block 사이의 공백 문제](http://css-tricks.com/fighting-the-space-between-inline-block-elements/)를 해결해야 합니다. 더구나 이 문제에 대한 모든 [해결방법](http://davidwalsh.name/remove-whitespace-inline-block)은 [더럽거나](https://github.com/suitcss/components-grid/blob/master/lib/grid.css#L30) [성가십니다](https://twitter.com/thierrykoblentz/status/305152267374428160).

Flexbox는 이러한 문제를 해결할 뿐만 아니라, 완전히 새로운 가능성의 세상을 열었습니다.

## Flexbox 그리드 시스템의 기능

그리드 시스템은 종종 수 많은 크기 옵션을 제공합니다. 하지만 대다수의 경우 두 세개의 요소를 나란히 배치하기만 하면 됩니다. 그렇다면, 왜 우리는 모든 각각의 셀(Cell)에 크기를 지정하는 클래스를 필요로 해야할까요?

아래의 리스트는 이상적인 그리드 시스템에 대한 저의 기준입니다. 다행히도, Flexbox를 사용하면 이러한 기능의 대부분을 아주 쉽게 구현할 수 있습니다.

- 같은 행에 있는 그리드 셀은 기본 값으로 같은 너비 및 높이를 가집니다. 기본적으로 크기가 공간에 들어맞습니다.
- 보다 세밀한 제어를 위해, 각각의 셀에 크기를 지정하는 클래스를 추가할 수 있습니다. 이러한 클래스가 없다면, 각 셀은 원래처럼 빈 공간을 알아서 나눕니다.
- 반응형 그리드를 위해, 미디어 쿼리 관련 클래스를 셀에 추가할 수 있습니다.
- 각각의 셀은 수직적으로 상단, 하단 및 중단으로 정렬할 수 있습니다.
- 그리드 내의 모든 셀에 동일한 크기나 미디어, 정렬 값을 지정하기 위해서 불필요한 반복을 하지않고, 컨테이너에 하나의 클래스를 추가하기만 하면 됩니다.
- 그리드는 원하는 만큼 깊게 중첩될 수 있습니다.


### 기본 그리드

아래 그리드 셀은 어떠한 너비값도 지정받지 않았습니다. 자연스럽게 스스로 같은 공간을 가지고 행 전체로 확장되었습니다. 또한 기본적으로 높이 값이 같습니다.

<div class="Grid Grid--gutters u-textCenter">
  <div class="Grid-cell">
    <div class="Demo">1/2</div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">1/2</div>
  </div>
</div>

<div class="Grid Grid--gutters u-textCenter">
  <div class="Grid-cell">
    <div class="Demo">1/3</div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">1/3</div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">1/3</div>
  </div>
</div>

<div class="Grid Grid--gutters u-textCenter">
  <div class="Grid-cell">
    <div class="Demo">1/4</div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">1/4</div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">1/4</div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">1/4</div>
  </div>
</div>

<div class="Grid Grid--gutters Grid--flexCells">
  <div class="Grid-cell">
    <div class="Demo">
      컨텐츠가 공간을 메우지 않아도, 꽉찬 높이 값을 가집니다.
    </div>
  </div>

  <div class="Grid-cell">
    <div class="Demo">
      Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum mollis velit non gravida venenatis. Praesent consequat lectus purus, ut scelerisque velit condimentum eu. Maecenas sagittis ante ut turpis varius interdum. Quisque tellus ipsum, eleifend non ipsum id, suscipit ultricies neque.
    </div>
  </div>
</div>

### 개별 사이징

모두 같은 너비를 가지는 것을 원하지 않는다면, 각각의 셀에 크기를 지정하는 클래스를 추가할 수 있습니다. 사이즈를 지정하는 클래스가 없는 셀들은 간단히 원래대로 남은 공간을 나누어 가집니다.

"auto"이라는 단어가 붙은 셀은 사이즈를 지정하는 클래스가 없는 셀입니다.

<div class="Grid Grid--gutters u-textCenter">
  <div class="Grid-cell u-1of2">
    <div class="Demo">1/2</div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">auto</div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">auto</div>
  </div>
</div>

<div class="Grid Grid--gutters u-textCenter">
  <div class="Grid-cell">
    <div class="Demo">auto</div>
  </div>
  <div class="Grid-cell u-1of3">
    <div class="Demo">1/3</div>
  </div>
</div>

<div class="Grid Grid--gutters u-textCenter">
  <div class="Grid-cell u-1of4">
    <div class="Demo">1/4</div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">auto</div>
  </div>
  <div class="Grid-cell u-1of3">
    <div class="Demo">1/3</div>
  </div>
</div>

### 반응형

반응형 그리드는 그리드 셀 혹은 컨테이너에 미디어 클래스를 추가함으로서 동작합니다. 이러한 미디어 값이 충족되면 그리드는 자동적으로 적절히 조정됩니다.

아래에 있는 셀들은 기본적으로 꽉찬 너비를 가져야하고 `48em` 이상에 맞춰 확장됩니다. 실제 동작을 보기 위해서 브라우저 크기를 조절해보세요.

<div class="Grid Grid--gutters Grid--full large-Grid--fit u-textCenter">
  <div class="Grid-cell">
    <div class="Demo">Full / Halves</div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">Full / Halves</div>
  </div>
</div>
<div class="Grid Grid--gutters Grid--full large-Grid--fit u-textCenter">
  <div class="Grid-cell">
    <div class="Demo">Full / Thirds</div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">Full / Thirds</div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">Full / Thirds</div>
  </div>
</div>

### Grid-ception

그리드 컴포넌트끼리 무한으로 중첩할 수 있습니다.

<div class="Grid Grid--gutters Grid--flexCells u-textCenter">
  <div class="Grid-cell">
    <div class="Demo">
      <div class="Grid Grid--gutters u-textCenter">
        <div class="Grid-cell u-1of3">
          <div class="Demo">1/3</div>
        </div>
        <div class="Grid-cell">
          <div class="Demo">
            <div class="Grid Grid--gutters u-textCenter">
              <div class="Grid-cell">
                <div class="Demo">1/2</div>
              </div>
              <div class="Grid-cell">
                <div class="Demo">1/2</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="Grid-cell u-1of3">
    <div class="Demo">1/3</div>
  </div>
</div>

## 정렬 기능

### 그리드 셀 상단 정렬

<div class="Grid Grid--gutters Grid--top">
  <div class="Grid-cell">
    <div class="Demo">
      이 셀은 상단에 정렬됩니다.
    </div>
  </div>
  <div class="Grid-cell u-1of2">
    <div class="Demo">
      Pellentesque sagittis vel erat ac laoreet. Phasellus ac aliquet enim, eu aliquet sem. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed pulvinar porta leo, eu ultricies nunc sollicitudin vitae. Curabitur pulvinar dolor lectus, quis porta turpis ullamcorper nec. Quisque eget varius turpis, quis iaculis nibh.
    </div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">
      이 셀은 상단에 정렬됩니다.
    </div>
  </div>
</div>

### 그리드 셀 하단 정렬

<div class="Grid Grid--gutters Grid--bottom">
  <div class="Grid-cell">
    <div class="Demo">
      이 셀은 하단에 정렬됩니다.
    </div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">
      Curabitur pulvinar dolor lectus, quis porta turpis ullamcorper nec. Quisque eget varius turpis, quis iaculis nibh. Ut interdum ligula id metus hendrerit cursus. Integer eu leo felis. Aenean commodo ultrices nunc, sit amet blandit elit gravida in.
    </div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">
      이 셀은 하단에 정렬됩니다.
    </div>
  </div>
</div>

### 그리드 셀 수직 중앙 정렬

<div class="Grid Grid--gutters Grid--center">
  <div class="Grid-cell">
    <div class="Demo">
      이 셀은 오른쪽에 있는 셀의 수직 중앙으로 정렬됩니다.
    </div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">
      Curabitur pulvinar dolor lectus, quis porta turpis ullamcorper nec. Quisque eget varius turpis, quis iaculis nibh. Ut interdum ligula id metus hendrerit cursus. Integer eu leo felis. Aenean commodo ultrices nunc, sit amet blandit elit gravida in. Sed est ligula, ornare ac nisi adipiscing, iaculis facilisis tellus. Nullam vel facilisis libero. Duis semper lobortis elit, vitae dictum erat.</div>
  </div>
</div>

### 수직 정렬 섞기

<div class="Grid Grid--gutters">
  <div class="Grid-cell Grid-cell--top">
    <div class="Demo">
      이 셀은 상단에 정렬됩니다.
    </div>
  </div>
  <div class="Grid-cell">
    <div class="Demo">
      Curabitur pulvinar dolor lectus, quis porta turpis ullamcorper nec. Quisque eget varius turpis, quis iaculis nibh. Ut interdum ligula id metus hendrerit cursus. Integer eu leo felis. Aenean commodo ultrices nunc, sit amet blandit elit gravida in. Sed est ligula, ornare ac nisi adipiscing, iaculis facilisis tellus.</div>
  </div>
  <div class="Grid-cell Grid-cell--center">
    <div class="Demo">
      이 셀은 중단에 정렬됩니다.
    </div>
  </div>
  <div class="Grid-cell Grid-cell--bottom">
    <div class="Demo">
      이 셀은 하단에 정렬됩니다.
    </div>
  </div>
</div>

## HTML

```html
<div class="Grid">
  <div class="Grid-cell">…</div>
  <div class="Grid-cell">…</div>
  <div class="Grid-cell">…</div>
</div>
```

## CSS

### 기본 그리드 스타일

```css
.Grid {
  display: flex;
}

.Grid-cell {
  flex: 1;
}
```

### 그리드 스타일 수정자(modifier)

```css
/* With gutters */
.Grid--gutters {
  margin: -1em 0 0 -1em;
}
.Grid--gutters > .Grid-cell {
  padding: 1em 0 0 1em;
}

/* Alignment per row */
.Grid--top {
  align-items: flex-start;
}
.Grid--bottom {
  align-items: flex-end;
}
.Grid--center {
  align-items: center;
}

/* Alignment per cell */
.Grid-cell--top {
  align-self: flex-start;
}
.Grid-cell--bottom {
  align-self: flex-end;
}
.Grid-cell--center {
  align-self: center;
}
```

### 반응형 수정자 (모바일 퍼스트 접근)

```css
/* Base classes for all media */
.Grid--fit > .Grid-cell {
  flex: 1;
}
.Grid--full > .Grid-cell {
  flex: 0 0 100%;
}
.Grid--1of2 > .Grid-cell {
  flex: 0 0 50%
}
.Grid--1of3 > .Grid-cell {
  flex: 0 0 33.3333%
}
.Grid--1of4 > .Grid-cell {
  flex: 0 0 25%
}

/* Small to medium screens */
@media (min-width: 24em) {
  .small-Grid--fit > .Grid-cell {
    flex: 1;
  }
  .small-Grid--full > .Grid-cell {
    flex: 0 0 100%;
  }
  .small-Grid--1of2 > .Grid-cell {
    flex: 0 0 50%
  }
  .small-Grid--1of3 > .Grid-cell {
    flex: 0 0 33.3333%
  }
  .small-Grid--1of4 > .Grid-cell {
    flex: 0 0 25%
  }
}

/* Large screens */
@media (min-width: 48em) {
  .large-Grid--fit > .Grid-cell {
    flex: 1;
  }
  .large-Grid--full > .Grid-cell {
    flex: 0 0 100%;
  }
  .large-Grid--1of2 > .Grid-cell {
    flex: 0 0 50%
  }
  .large-Grid--1of3 > .Grid-cell {
    flex: 0 0 33.3333%
  }
  .large-Grid--1of4 > .Grid-cell {
    flex: 0 0 25%
  }
}
```

이 데모에서 쓰인 그리드 컴포넌트의 전체 [소스 코드](https://github.com/philipwalton/solved-by-flexbox/blob/master/assets/css/components/grid.css)는 GitHub에서 보실 수 있습니다.
