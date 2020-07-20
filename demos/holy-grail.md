---
template: holy-grail.html
title: 성배 레이아웃
excerpt: 이 전형적인 문제는 CSS 해커들이 몇 년간 해결하려 노력했지만, 아직까지 유의미한 해결책은 나오지 않았습니다. Flexbox를 사용하면, 마침내 해결이 가능합니다.
---

[성배 레이아웃(Holy Grail Layout)](http://en.wikipedia.org/wiki/Holy_Grail_(web_design))은 시간이 지나면서 다양한 해결방법이 제시된 전형적인 CSS 문제입니다. 만약 성배 레이아웃의 역사에 대해 잘 모르신다면 그에 대한 좋은 요약과 더 잘 알려진 해결 방법을 다루는 [A List Apart의 글](http://alistapart.com/article/holygrail)을 참고하세요.

성배 레이아웃의 핵심은 헤더(Header), 푸터(Footer)와 3개의 열(Column)로 구성된 페이지입니다. 중앙 열은 주요 내용을 담고, 왼쪽 및 오른쪽 열은 광고 혹은 네비게이션과 같이 보충하는 컨텐츠를 담습니다.

이 문제에 대한 대부분의 CSS 해결방법의 목적은 몇 가지 목표를 달성하는 것입니다.

- 중심은 유동적이고, 사이드바는 고정된 너비를 가져야 합니다.
- 가운데 열(주 컨텐츠)은 HTML 소스상에서 맨 앞에 있어야 합니다.
- 모든 열은 어떤 열이 실제로 제일 긴지에 관계 없이 같은 높이를 가져야 합니다.
- 최소한의 마크업만을 필요로 해야 합니다.
- 페이지의 내용이 부족할 때에도 푸터는 페이지 하단에 붙어야 합니다.

안타깝게도 이러한 목표의 성질과 원래 CSS의 한계 때문에, 이 문제에 대한 전통적인 해결법 중 아무 것도 이 모든 사항을 다 만족시킬 수는 없었습니다.

Flexbox를 사용하면, 마침내 완전한 해결방법이 가능합니다.

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

푸터를 하단에 붙이고 가운데 컨텐츠 행을 늘이는 방법은 [고정된 푸터](../sticky-footer/)에서 보여준 것과 같은 테크닉으로 풀 수 있습니다. 유일한 차이점은 성배 레이아웃의 가운데 행(`.HolyGrail-body`)이 `display:flex`여야 한다는 것 뿐입니다. 이는 가운데 행 자식들을 적절히 배열하기 위해서입니다.

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

중심이 가변이고, 사이드바는 고정폭인 같은 높이의 컬럼 세 개를 스타일링하는 것은 매우 쉽습니다.

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

### 반응형 만들기

성배 레이아웃은 거의 모든 사람들이 컴퓨터로 브라우징을 하던 시대의 것입니다. 하지만 모바일 기기가 증가하고 반응형 디자인이 떠오르면서 성배 레이아웃은 거의 유행에 뒤처지게 되었습니다.

어쨌든, Flexbox를 사용하면 모바일 퍼스트 혹은 모바일 친화적인 버전의 성배 레이아웃을 만드는 것도 쉽습니다. 요점은 가운데 섹션을 기본적으로 `flex-direction:column`으로 만들고, 큰 화면을 위해서는 `flex-direction:row`를 사용하는 것입니다.

여기 반응형이면서 모바일 퍼스트인 완벽한 예제가 있습니다. 브라우저 창의 크기를 조절함으로써 실제로 어떻게 동작하는 지 볼 수 있습니다.

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

이 데모에서 사용한 `HolyGrail` 컴포넌트의 [소스 코드](https://github.com/philipwalton/solved-by-flexbox/blob/master/assets/css/components/grid.css)를 Github에서 확인해 보세요.
