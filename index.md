帰ってきたYokohama.js (#yjs20140419)

## JavaScriptでKeyframeAnimationを<br>作ってみた

---

## 自己紹介
![](https://avatars2.githubusercontent.com/u/730940?s=200)

宇野 陽太([@cancer6](https://twitter.com/cancer6))

株式会社モバイルファクトリーというところで<br>
フロントエンドエンジニアやってます

最近はBackbone / Marionette / AngularJS あたりを触ったり<br>
CSS書いたりなど

---

## CSS Animation

---

### CSS Animation

- CSSにkeyframe書いて...
- アニメーション用のclassを作ってプロパティ書いて...
- JSからclassの操作して...
- ...

---

## めんどくさい

---

## どうせJS使うなら全部JSでやってしまおう

---

### css-animations.js

https://github.com/jlongster/css-animations.js

- DOMからCSSにアクセスして色々やってくれる
 - CSSファイルで定義したkeyframeを取ってきたり
 - JavaScriptから動的にkeyframeを生成したり
- オブジェクトでkeyframeのプロパティを渡してあげる

```javascript
var anim1 = CSSAnimations.get("anim1");
var anim2 = CSSAnimations.create("anim2", {
    "0%": { "background-color": "red" },
    "100%": { "background-color": "blue" }
```

--

### css-animations.js

- ベンダープレフィックスが必要なプロパティの記述が冗長
 - transform系のプロパティも冗長になりがち
- アニメーションのプロパティ(animation-name/animation-durationなど)は別途DOMの操作が必要

```javascript
var anim = CSSAnimations.create("anim", {
    "0%": {
      opacity: "0.5",
      border-radius: "0"
      "-webkit-border-radius": "0"
      transform: "translate(0, 0) rotate(90deg) scale(1)"
      "-webkit-transform": "translate(0, 0) rotate(90deg) scale(1)"
    },
    "100%": {
      opacity: "1",
      border-radius: "5px"
      "-webkit-border-radius": "5px"
      transform: "translate(100px, 50px) rotate(180deg) scale(2)"
      "-webkit-transform": "translate(100px, 50px) rotate(180deg) scale(2)"
    }

$("#animation").css({
  "animation-name": "anim",
  "animation-duration": "5s"
  "animation-timing-function": "linear"
  "animation-delay": "1s"
  "animation-fill-mode": "both"
});
```

---

## まだめんどくさい

---

### keyframe-animations.js ｶｯｺｶﾘ

https://github.com/cancer/keyframe-animations.js

- (さっき)つくりました
- No more ベンダープレフィックス
- transform系も見やすく
- アニメーションのプロパティも一緒に設定できます

```javascript
var animation = keyframeAnimation.setup({
  name: "anim",
  keyframe: {
    "0%": {
      opacity: "0.5",
      borderRadius: "0",
      translate: "0 0",
      rotate: "90deg",
      scale: "1"
    },
    "100%": {
      opacity: "1",
      borderRadius: "5px",
      translate: "100px 50px",
      rotate: "180deg",
      scale: "2"
    }
  },
  animation: {
    duration: "5s",
    timingFunction: "linear",
    delay: "1s",
    fillMode: "both"
  }
});
```

--

### keyframe-animations.js ｶｯｺｶﾘ

- アニメーションの実行/停止もかんたん
 - animationEndで何かしたいとかもできます

```javascript
// アニメーション実行
animation.animate($("#animation"));

// アニメーション停止
animation.freeze();

// animationEndで何か実行したい
animation.animate($("#animation"), function($element){
  // アニメーションが終わったら要素を非表示にする
  $element.hide()
});
```

--

### keyframe-animations.js ｶｯｺｶﾘ

- アニメーションのライブラリを作ったりすると捗るはず

![](http://i.gyazo.com/90622a58e2134b64bfdf3dc47111899e.png)

```javascript
var animationLibrary = new AnimationLibrary();
animationLibrary.setupModalAnimation();
```
こんな感じで

---

### ご清聴ありがとうございました

