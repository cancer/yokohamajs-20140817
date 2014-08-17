Yokohama.js (#yjs20140817)

#CSS Spriteを動的生成して快適ソシャゲ開発

---

## 自己紹介
![](https://avatars2.githubusercontent.com/u/730940?s=200)

宇野 陽太([@cancer6](https://twitter.com/cancer6))

株式会社モバイルファクトリーというところで<br>
フロントエンドエンジニアやってます

最近はBackbone / Marionette / AngularJS あたりを触ったり<br>
CSSの設計したりなど

---

# 流れ
- Image Assets Generatorで画像を書き出す
- Compassが監視してるフォルダに配置する
- Compass watch

---

## Image Assets Generatorで画像を書き出す

- [ファイル] → [生成]にチェックを入れておく
- レイヤーにファイル名をつけておく
- レイヤーが更新されると指定した名前で自動的に書き出し
- ※ Photoshop CC以降

---

## Compassが監視してるフォルダに配置する

- 職人が丹精込めて一つ一つ移動

---

## Compass watch

- CSSの生成と一緒にSpriteファイルも生成してくれる
- 便利！

---

# CSS Sprite Helpers for Compass

http://compass-style.org/reference/compass/helpers/sprites/

---

## CSS Sprite Helpers(略)のいいところ

- 導入が楽
 - Compassが用意しているfunctionを使えばすぐ
 - Sass(SCSS)ファイルに書いていくだけ

---

## CSS Sprite Helpers(略)のよくないところ

- 謎い
 - マッピング情報はRuby側で管理
 - functionで取得するのでキャッシュしておかないといけない

--

- 遅い
 - CSSの生成が遅くなる(画像の変更が無くても+数秒)
 - Sass(SCSS)に変更があるたびに画像の差分をチェック
 - (Spriteの生成が遅いわけではないです、たぶん)

--

- 画像生成後にgrunt-watchが走らない
 - 画像の最適化とかしてると地味につらい

---

# grunt-spritesmith

https://github.com/Ensighten/grunt-spritesmith

---

## grunt-spritesmithのいいところ

- Compass...というかSassに非依存
 - LESSでもStylusでも使える
- CSSの生成とCSS Spriteの生成を分離できる
 - CompassはCSSの生成に集中
 - CSSの生成が早くなる

--

- Compassみたいにブラックボックスじゃない
 - マッピング情報はSass(SCSS)の変数化される
 - 変数にアクセスするfunctionも一緒に書きだされる

---

## grunt-spritesmithのよくないところ

- フォルダが分けられない
 - 一つのフォルダを監視して一つのSpriteを生成する
- CompassのI/Fと差異があるので、途中からの移行がつらい
 - 規模が大きくなってくると全部差し替えとかやってられない

---

## もう少し使いやすく...

- 複数のフォルダを監視するgruntTaskを作成
 - 対象のフォルダ以下にあるフォルダ名でSpriteファイルを生成
 - grunt-spritesmithが作るマッピング情報をJSONで保存
 - パースしてSass(SCSS)のMapに変換
- 既存のI/Fを再利用

---

## 今後やりたいこと
- Image Assets GeneratorとCLIの連携
 - 職人のぬくもりを機械で置き換えたい

---

### ご清聴ありがとうございました

