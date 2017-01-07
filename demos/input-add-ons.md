---
template: default.html
title: Input 추가 요소
excerpt: 꽉찬 너비를 가진 유연한 input/버튼 쌍을 만드는 것은 지금까지의 CSS로는 거의 불가능했습니다. Flexbox는 이를 구현하는 가장 쉬운 방법입니다.
---

CSS에서 input의 크기가 조절되는 방식 때문에, input의 앞이나 뒤에 다른 추가 요소(Add-on)를 더하고 input이 유연하게 빈 공간을 채우도록 동작하게 만드는 것은 거의 불가능했습니다.

이를 해결하기 위해 존재하는 방법이란 input의 너비를 정확하게 알고 있거나, 그 자체로 많은 문제를 안고 있는 `display:table-cell` 같은 것을 사용하는 방법 뿐입니다. 그중에서 특히 특정 브라우저에서는 추가 요소 내부에 어떤 것을 절대적으로 위치시키는 것이 매우 어렵습니다.

Flexbox를 사용하면, 이런 문제들은 모두 사라지고 코드도 간단해집니다. 게다가, 자동으로 input 필드와 추가 요소의 높이도 같아집니다.

<div class="Grid Grid--guttersLg Grid--full med-Grid--fit">
  <div class="Grid-cell">
    <h2>앞 쪽의 추가 요소</h2>
    <div class="InputAddOn">
      <span class="InputAddOn-item">Amount</span>
      <input class="InputAddOn-field">
    </div>
    <div class="InputAddOn">
      <button class="InputAddOn-item"><span class="icon icon-search"></span></button>
      <input class="InputAddOn-field">
    </div>
  </div>
  <div class="Grid-cell">
    <h2>뒤 쪽의 추가 요소</h2>
    <div class="InputAddOn">
      <input class="InputAddOn-field">
      <button class="InputAddOn-item">Go</button>
    </div>
    <div class="InputAddOn">
      <input class="InputAddOn-field">
      <button class="InputAddOn-item"><span class="icon icon-star"></span></button>
    </div>
  </div>
</div>

## 양 쪽의 추가요소

<div class="Grid Grid--guttersLg Grid--full med-Grid--fit">
  <div class="Grid-cell">
    <div class="InputAddOn">
      <span class="InputAddOn-item"><span class="icon icon-envelope"></span></span>
      <input class="InputAddOn-field" placeholder="Example One">
      <button class="InputAddOn-item">Send</button>
    </div>
  </div>
  <div class="Grid-cell">
    <div class="InputAddOn">
      <span class="InputAddOn-item"><span class="icon icon-lock"></span></span>
      <input class="InputAddOn-field" placeholder="Example One">
      <button class="InputAddOn-item">Encrypt</button>
    </div>
  </div>
</div>

## HTML

```html
<!-- 앞 쪽에 추가 -->
<div class="InputAddOn">
  <input class="InputAddOn-field">
  <button class="InputAddOn-item">…</button>
</div>

<!-- 뒤 쪽에 추가 -->
<div class="InputAddOn">
  <span class="InputAddOn-item">…</span>
  <input class="InputAddOn-field">
</div>

<!-- 양 쪽에 추가 -->
<div class="InputAddOn">
  <span class="InputAddOn-item">…</span>
  <input class="InputAddOn-field">
  <button class="InputAddOn-item">…</button>
</div>
```

## CSS

```css
.InputAddOn {
  display: flex;
}

.InputAddOn-field {
  flex: 1;
  /* field styles */
}

.InputAddOn-item {
  /* item styles */
}

```

이 데모에서 Input 추가요소를 위해 쓰인 전체 [소스 코드](https://github.com/philipwalton/solved-by-flexbox/blob/master/assets/css/components/grid.css)는 GitHub에서 보실 수 있습니다.
