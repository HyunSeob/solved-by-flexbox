---
template: default.html
title: 수직 중앙 정렬
excerpt: 이 전형적인 문제는 CSS 해커들이 몇 년간 해결하려 노력했지만, 아직까지 유의미한 해결책은 나오지 않았습니다. Flexbox를 사용하면, 마침내 해결이 가능합니다.
---

CSS에서 요소를 수직적으로 중앙에 정렬하는 좋은 방법이 없다는 것은 CSS 전체를 평가하는 데 있어서 큰 흠집이었습니다.

문제를 더 크게 만드는 것은 수직 중앙 정렬을 위한 테크닉들이 모호하고 직관적이지 않다는 것이었습니다. 오히려 명백한 코드(`vertical-align:middle` 같은)는 원할 때는 제대로 동작하지 않는 것처럼 보이는데 말이죠.

현재 수직 중앙 정렬을 위해 시도할 수 있는 것들은 margin을 음수 값으로 주는 것부터, `display:table-cell` 혹은 가상 요소(pseudo-element)에 꽉찬 높이를 주는 등 어처구니없는 핵(hack)들입니다. 때로는 이런 테크닉을 이용해 일을 마무리했겠지만, 이런 테크닉들은 어떤 상황에는 동작하지 않습니다. 만약 중앙으로 정렬하고 싶은 요소의 크기를 알지 못하고, 그 요소가 부모의 유일한 자식이 아닐경우 어떻게 해야할까요? 가상 요소를 사용해서 해결한 경우, 그 가상 요소를 다른 용도로 써야하는 경우에는 어떻게 해야할까요?

Flexbox와 함께라면 더 이상 걱정할 필요가 없습니다. 이제 어떤 것(수직이든 수평이든)이라도 `align-items`, `align-self`, 'justify-content'를 사용하면 힘들이지 않고 정렬할 수 있습니다.

<div class="Demo Demo--spaced u-ieMinHeightBugFix">
  <div class="Aligner">
    <div class="Aligner-item Aligner-item--fixed">
      <div class="Demo">
        <h3>중앙 정렬됨!</h3>
        <p contenteditable="true"> 이 박스는 수직, 수평 중앙 정렬되었습니다. 이 박스의 텍스트가 넓어지거나 커지더라도 여전히 중앙 정렬됩니다. 한 번 시도해보세요. 그냥 클릭 후 텍스트를 수정하면 됩니다.</p>
      </div>
    </div>
  </div>
</div>

기존의 특정 수직 정렬 테크닉과는 다르게, Flexbox를 사용하면 수직 정렬이 다른 형제 요소에 영향을 미치지 않습니다.

<div class="Demo Demo--spaced u-ieMinHeightBugFix">
  <div class="Aligner">
    <div class="Aligner-item Aligner-item--top">
      <div class="Demo"><strong>Top</strong></div>
    </div>
    <div class="Aligner-item">
      <div class="Demo"><strong>Centered</strong></div>
    </div>
    <div class="Aligner-item Aligner-item--bottom">
      <div class="Demo"><strong>Bottom</strong></div>
    </div>
  </div>
</div>

## HTML

```html
<div class="Aligner">
  <div class="Aligner-item Aligner-item--top">…</div>
  <div class="Aligner-item">…</div>
  <div class="Aligner-item Aligner-item--bottom">…</div>
</div>
```

## CSS

```css
.Aligner {
  display: flex;
  align-items: center;
  justify-content: center;
}

.Aligner-item {
  max-width: 50%;
}

.Aligner-item--top {
  align-self: flex-start;
}

.Aligner-item--bottom {
  align-self: flex-end;
}
```

이 데모에서 `Aligner` 컴포넌트를 위해 쓰인 모든 [소스 코드](https://github.com/philipwalton/solved-by-flexbox/blob/master/assets/css/components/aligner.css)는 GitHub에서 보실 수 있습니다.

<aside class="Notice"><strong>주의:</strong>&nbsp; 이 데모를 크로스 브라우저에서 동작하도록 만드는 CSS는 위의 예제와는 약간 다릅니다. 위의 예제는 스펙이 완전히 구현된 브라우저를 가정합니다. 자세한 내용은 이 <a href="https://github.com/philipwalton/solved-by-flexbox/blob/master/assets/css/utils/compat.css">소스 코드</a>의 주석 부분을 참고해주시기 바랍니다.</aside>
