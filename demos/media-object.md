---
template: default.html
title: 미디어 객체
excerpt: 오버플로우, clearfix 혹은 블록 서식 문맥에 대한 걱정없이 고정되거나 다양한 크기의 이미지를 가진 미디어 객체를 만듭니다.
---

[미디어 객체](http://www.stubbornella.org/content/2010/06/25/the-media-object-saves-hundreds-of-lines-of-code)는 객체지향 CSS(OOCSS)의 전형적인 결과물입니다. 그 단순함과 활용성은 많은 CSS 개발자(저를 포함해서)를 OOCSS 방법론으로 전향시켰습니다.

하지만 대부분의 CSS 레이아웃 테크닉과 흡사하게도, 미디어 객체는 그 목표를 달성하기 위해서 트릭이나 핵(hack)에 의존해야 합니다.

미디어 객체의 내부는 [블록 서식 문맥](http://www.stubbornella.org/content/2013/07/31/re-visiting-the-secret-power-of-block-fomatting-context/)을 생성하거나 왼쪽 마진/패딩을 이미지의 폭과 똑같이 줌으로써, 이미지 때문에 텍스트가 덮여버리는 일을 방지해야합니다. 또한 미디어 객체는 `overflow:hidden` 혹은 가상 요소(pseudo-element)를 사용하여 clearfix하는 것이 필요합니다.

Flexbox와 함께라면 이런 문제들은 모두 해결됩니다. 게다가, Flexbox를 사용하면 미디어 객체의 이미지를 원하는 대로 정렬시킬 수 있습니다. 또한, 코드의 순서를 변경하지 않아도 이미지를 우측으로 쉽게 정렬시킬 수도 있습니다.

## 기본 예제

<div class="Grid Grid--guttersLg Grid--full large-Grid--fit">
  <div class="Grid-cell">
    <div class="Demo Demo--spaced">
      <div class="Media">
        <img class="Media-figure Image" src="{{ site.baseUrl }}images/kitten.jpg" alt="Kitten">
        <div class="Media-body">
          <h3 class="Media-title">표준 미디어 객체</h3>
          <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur ac nisl quis massa vulputate adipiscing. Vivamus sit amet risus ligula. Nunc eu pulvinar augue.</p>
        </div>
      </div>
    </div>
    <div class="Demo Demo--spaced">
      <div class="Media">
        <img class="Media-figure Image" src="{{ site.baseUrl }}images/kitten.jpg" alt="Kitten">
        <div class="Media-body">
          <h3 class="Media-title">표준 미디어 객체</h3>
          <p>Donec imperdiet sem leo, id rutrum risus aliquam vitae. Cras tincidunt porta mauris, vel feugiat mauris accumsan eget.</p>
        </div>
      </div>
    </div>
  </div>
  <div class="Grid-cell">
    <div class="Demo Demo--spaced">
      <div class="Media Media--reverse">
        <img class="Media-figure Image" src="{{ site.baseUrl }}images/kitten.jpg" alt="Kitten">
        <div class="Media-body">
          <h3 class="Media-title">뒤집힌 미디어 객체</h3>
          <p>Phasellus vel felis purus. Aliquam consequat pellentesque dui, non mollis erat dictum sit amet. Curabitur non quam dictum, consectetur arcu in, vehicula justo. Donec tortor massa, eleifend nec viverra in, aliquet at eros. Mauris laoreet condimentum mauris, non tempor massa fermentum ut. Integer gravida pharetra cursus. Nunc in suscipit nunc.</p>
        </div>
      </div>
    </div>
  </div>
</div>

## 이미지가 아닌 경우

<div class="Grid Grid--guttersLg Grid--full large-Grid--fit">
  <div class="Grid-cell">
    <div class="Demo Demo--spaced">
      <div class="Media">
        <figure class="Media-figure"><span class="icon-comments icon-big"></span></figure>
        <div class="Media-body">
          <h3 class="Media-title">아이콘 사용</h3>
          <p>Donec imperdiet sem leo, id rutrum risus aliquam vitae. Vestibulum ac turpis non lacus dignissim dignissim eu sed dui.</p>
        </div>
      </div>
    </div>
  </div>
  <div class="Grid-cell">
    <div class="Demo Demo--spaced">
      <div class="Media Media--center">
        <figure class="Media-figure"><span class="icon-info-sign icon-big"></span></figure>
        <div class="Media-body">
          <h3 class="Media-title">중앙 정렬된 아이콘</h3>
          <p>Nunc nec fermentum dolor. Duis at iaculis turpis. Sed rutrum elit ac egestas dapibus. Duis nec consequat enim.</p>
        </div>
      </div>
    </div>
  </div>
</div>

## 중첩된 미디어 객체

<div class="Grid Grid--guttersLg Grid--full large-Grid--fit">
  <div class="Grid-cell">
    <div class="Demo Demo--spaced">
      <div class="Media">
        <img class="Media-figure Image" src="{{ site.baseUrl }}images/kitten.jpg" alt="Kitten">
        <div class="Media-body">
          <h3 class="Media-title">미디어 객체 제목</h3>
          <p>Phasellus vel felis purus. Aliquam consequat pellentesque dui, non mollis erat dictum sit amet. Curabitur non quam dictum, consectetur arcu in, vehicula justo.</p>
          <div class="Demo Demo--spaced u-smaller">
            <div class="Media">
              <figure class="Media-figure">
                <img class="Image Image--tiny" src="{{ site.baseUrl }}images/kitten.jpg" alt="Kitten">
              </figure>
              <p class="Media-body">
                Mauris porta arcu id magna adipiscing lacinia at congue lacus. Vivamus blandit quam quis tincidunt egestas. Etiam posuere lectus sed sapien malesuada molestie.
              </p>
            </div>
          </div>
          <div class="Demo Demo--spaced u-smaller">
            <div class="Media">
              <figure class="Media-figure">
                <img class="Image Image--tiny" src="{{ site.baseUrl }}images/kitten.jpg" alt="Kitten">
              </figure>
              <div class="Media-body">
                <p>Vestibulum ac turpis non lacus dignissim dignissim eu sed dui. Proin a ligula sit amet massa malesuada mattis eu a ante. Nunc porttitor sed quam quis sollicitudin. Vestibulum ac turpis non lacus dignissim dignissim eu sed dui.</p>
                <div class="Media Media--center">
                  <span class="Media-figure icon-thumbs-up-alt"></span>
                  <p class="Media-body">Rutrum risus aliquam vitae.</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="Grid-cell">
    <div class="Demo Demo--spaced">
      <div class="Media">
        <img class="Media-figure Image" src="{{ site.baseUrl }}images/kitten.jpg" alt="Kitten">
        <div class="Media-body">
          <h3 class="Media-title">미디어 객체 제목</h3>
          <p>Phasellus vel felis purus. Aliquam consequat pellentesque dui, non mollis erat dictum sit amet. Curabitur non quam dictum, consectetur arcu in, vehicula justo. Donec tortor massa, eleifend nec viverra in, aliquet at eros. Mauris laoreet condimentum mauris, non tempor massa fermentum ut.</p>
          <div class="Media Media--center u-smaller">
            <span class="Media-figure icon-thumbs-up-alt"></span>
            <p class="Media-body">Donec imperdiet sem leo, id rutrum risus aliquam vitae.</p>
          </div>
          <div class="Demo Demo--spaced u-smaller">
            <div class="Media">
              <figure class="Media-figure">
                <img class="Image Image--tiny" src="{{ site.baseUrl }}images/kitten.jpg" alt="Kitten">
              </figure>
              <p class="Media-body">
                Mauris porta arcu id magna adipiscing lacinia at congue lacus. Vivamus blandit quam quis tincidunt egestas. Etiam posuere lectus sed sapien malesuada molestie. Aliquam vitae pharetra dolor. Nullam non mattis nunc.
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

## HTML

```html
<div class="Media">
  <img class="Media-figure" src="" alt="">
  <p class="Media-body">&hellip;</p>
</div>
```

## CSS

```css
.Media {
  display: flex;
  align-items: flex-start;
}

.Media-figure {
  margin-right: 1em;
}

.Media-body {
  flex: 1;
}
```

이 데모에서 미디어 객체 컴포넌트를 위해 사용된 모든 [소스 코드](https://github.com/philipwalton/solved-by-flexbox/blob/master/assets/css/components/media.css)는 GitHub에서 보실 수 있습니다.
