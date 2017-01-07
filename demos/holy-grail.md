---
template: holy-grail.html
title: 성배 레이아웃
excerpt: 이 전형적인 문제는 CSS 해커들이 몇 년간 해결하려 노력했지만, 아직까지 유의미한 해결책은 나오지 않았습니다. Flexbox를 사용하면, 마침내 해결이 가능합니다.
---

[성배 레이아웃(Holy Grail Layout)](http://en.wikipedia.org/wiki/Holy_Grail_(web_design))은 시간에 따라 다양한 해결방법이 나타난 전형적인 CSS 문제입니다. 만약 성배 레이아웃의 역사에 대해 잘 모르신다면 좋은 요약과 잘 알려진 해결방법을 다루는 [A List Apart의 글](http://alistapart.com/article/holygrail)을 참고하세요.

성배 레이아웃의 핵심은 헤더(Header), 푸터(Footer)와 3개의 열(Column)으로 구성된 페이지 레이아웃이라는 것입니다. 중앙에 있는 열은 주요 내용을 담고, 왼쪽 및 오른쪽 열은 내용을 보충하는 광고 혹은 네비게이션을 포함합니다.

이 문제에 대한 대부분의 CSS 해결방법은 몇 가지 목표를 달성하는 것이 목표입니다.

- 중단 컨테이너는 유연한 크기를 가지고 사이드바는 고정된 너비를 가져야 합니다.
- 중단 열(주요 내용)은 HTML 소스상에서 가장 첫 번째에 있어야 합니다.
- 모든 열은 실제 높이에 관계 없이, 같은 높이를 가져야합니다.
- 최소한의 마크업만을 필요로 해야합니다.
- 페이지의 내용이 부족할 때에도 푸터는 하단에 고정되어있어야 합니다.

안타깝게도, 이러한 목표의 성격과 기존 CSS의 한계 때문에, 이 문제에 대한 전통적인 해결법은 모든 사항을 만족 시킬 수 없었습니다.

Flexbox를 사용하면, 마침내 완전한 해결방법이 가능하게 되었습니다.

## HTML

```html
<body class="HolyGrail">
  <header>…</header>
  <div class="HolyGrail-body">
    <main class="HolyGrail-content">…</main>
    <nav class="HolyGrail-nav">…</nav>
    <aside class="HolyGrail-ads">…</aside>
  </div>
  <footer>…</footer>
</body>
```

## CSS

푸터를 하단에 고정시키기 위해서 중앙 내용을 늘린 방법은 [고정된 푸터](../sticky-footer/)에서 보여준 예제와 같습니다. 성배 레이아웃 중단 행(`.HolyGrail-body`)의 유일한 차이점은 자식 요소들을 적절히 배열하기 위해 `display:flex`를 필요로 한다는 것뿐입니다.

```css
.HolyGrail {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
}

.HolyGrail-body {
  display: flex;
  flex: 1;
}
```

세 개의 동일한 높이의 열을 가지는 유연한 중단 영역과 고정된 너비의 사이드바를 만드는 것은 다음과 같이 매우 쉽습니다.

```css
.HolyGrail-content {
  flex: 1;
}

.HolyGrail-nav, .HolyGrail-ads {
  /* 12em은 열의 너비입니다. */
  flex: 0 0 12em;
}

.HolyGrail-nav {
  /* 좌측에 네비게이션을 놓습니다. */
  order: -1;
}
```

<aside class="Notice"><strong>주의:</strong>&nbsp; 이 데모를 크로스 브라우저에서 동작하도록 만드는 CSS는 위의 예제와는 약간 다릅니다. 위의 예제는 스펙이 완전히 구현된 브라우저를 가정합니다. 자세한 내용은 이 <a href="https://github.com/philipwalton/solved-by-flexbox/blob/master/assets/css/components/holy-grail.css">소스 코드</a>의 주석 부분을 참고해주시기 바랍니다.</aside>

### 반응형

성배 레이아웃은 웹 디자인이 컴퓨터에서 하는 브라우징만을 대응하던 시대의 것입니다. 하지만 모바일 기기가 증가하고 반응형 디자인이 떠오르면서 성배 레이아웃은 거의 유행에 뒤처지게 되었습니다.

어쨌든, Flexbox를 사용한다면 모바일 퍼스트 혹은 모바일 친화적인 버전의 성배 레이아웃을 만드는 것도 쉽습니다. 요점은 중단 섹션을 기본적으로 `flex-direction:column`을 사용해서 만들고 큰 스크린을 대응하기 위해 `flex-direction:row`를 사용하는 것입니다.

이 페이지는 반응형이며 모바일 퍼스트인 완전한 예제입니다. 브라우저 창의 크기를 조절함으로써 실제로 어떻게 동작하는 지 볼 수 있습니다.

```css
.HolyGrail,
.HolyGrail-body {
  display: flex;
  flex-direction: column;
}

.HolyGrail-nav {
  order: -1;
}

@media (min-width: 768px) {
  .HolyGrail-body {
    flex-direction: row;
    flex: 1;
  }
  .HolyGrail-content {
    flex: 1;
  }
  .HolyGrail-nav, .HolyGrail-ads {
    /* 12em은 열의 너비입니다. */
    flex: 0 0 12em;
  }
}
```

성배 레이아웃을 위해 쓰인 전체 [소스 코드](https://github.com/philipwalton/solved-by-flexbox/blob/master/assets/css/components/grid.css)를 확인해보세요.
