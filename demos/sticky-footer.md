---
template: default.html
title: 고정된 푸터
excerpt: 페이지의 내용이 충분히 차있지 않을 때 푸터를 하단에 고정시키는 건 항상 어려운 일이었습니다. 그리고 푸터의 높이를 알 수 없다면, 사실상 불가능합니다. 이젠 더 이상 불가능하지 않습니다.
---

<div class="Demo Demo--spaced">

이 페이지의 내용을 가리는 아래의 버튼을 눌러보십시오. 그리고 페이지가 내용으로 가득차있지 않음에도 불구하고 푸터(Footer)가 창의 하단에 고정되는 것을 확인하십시오.

<button id="collapse-trigger" class="Button"><span class="icon-refresh u-spaceRS"></span> 내용 토글하기</button>

</div>

<div id="collapsable-content">

페이지의 내용이 부족할 때 푸터를 하단에 고정시키는 것은 모든 웹 개발자가 한 번 쯤은 해보았을만한 것입니다. 그리고, 대부분의 경우 그 문제를 해결했을 것입니다. 그러나 기존에 [존재하던 해결방법](http://ryanfait.com/resources/footer-stick-to-bottom-of-page/)은 푸터의 높이를 모를 경우 쓸 수 없다는 심각한 단점이 있습니다.

Flexbox는 이러한 유형의 문제에 대한 완벽한 해답입니다. Flexbox는 내용을 수평 방향으로 배치하는데에 좋다고 알려져있지만, 실제로는 수직적인 레이아웃 문제를 위해서도 좋습니다. 해야할 일은 그저 수직적인 섹션들을 Flex 컨테이너로 감싸고, 확장할 섹션을 선택하기만 하면 됩니다. 그러면 섹션들은 자동적으로 컨테이너의 빈 공간을 채우게 될 것입니다.

아래의 예제에서는, 컨테이너가 브라우저 창의 크기로 설정되고, 내용 영역은 필요한 만큼 확장됩니다. *(주의: 수직 방향에서는 컨테이너의 높이를 지정해야합니다. 자동적으로 확장되는 수평 방향과는 다릅니다.)*

## HTML

```xml
<body class="Site">
  <header>…</header>
  <main class="Site-content">…</main>
  <footer>…</footer>
</body>
```

## CSS

```css
.Site {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
}

.Site-content {
  flex: 1;
}
```

이 데모에서 `Site` 컴포넌트를 위해 사용된 모든 [소스 코드](https://github.com/philipwalton/solved-by-flexbox/blob/master/assets/css/components/site.css)는 GitHub에서 보실 수 있습니다.

<aside class="Notice"><strong>주의:</strong>&nbsp; 이 데모를 크로스 브라우저에서 동작하도록 만드는 CSS는 위의 예제와는 약간 다릅니다. 위의 예제는 스펙이 완전히 구현된 브라우저를 가정합니다. 자세한 내용은 이 <a href="https://github.com/philipwalton/solved-by-flexbox/blob/master/assets/css/components/site.css">소스 코드</a>의 주석 부분을 참고해주시기 바랍니다.</aside>

</div>

<script class="js-allow-before-footer">
  (function() {
    var collapseTrigger = document.getElementById("collapse-trigger");
    var collapseableContent = document.getElementById("collapsable-content");
    var isCollapsed = false;
    collapseTrigger.addEventListener("click", function() {
      if (isCollapsed) {
        collapseableContent.classList.remove("u-hidden");
      } else {
        collapseableContent.classList.add("u-hidden");
      }
      isCollapsed = !isCollapsed;
    }, false);
  }());
</script>
