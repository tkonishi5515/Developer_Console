---
title: 開発者コンソールについて
marp: true
paginate: true
theme: freud
---

<!-- _paginate: false -->
<!-- theme: gradient class: blue-->
<!-- theme: freud class: blue-->

# 開発者コンソールについて <!-- fit -->

</br>
</br>

![Slides are here](images/QRCode.png)

##### スライド:https://tkonishi5515.github.io/Developer_Console/ja/index

##### リポジトリ:https://github.com/tkonishi5515/Developer_Console

---

# はじめに

#### 今回の話すこと

- 使い方をデモを含めて共有します
- vsCode の方が優れているところを共有します
- vsCode の詳細な設定方法は説明しません

---

# トピックス

1. 開発者コンソールとは
2. 開発者コンソールでできること
3. 非開発者にもおすすめな機能
4. ダミーデータ作成
5. 実践(demo)

---

# 開発者コンソールとは

## 基礎知識

[開発者コンソールの基礎](https://trailhead.salesforce.com/ja/content/learn/modules/developer_console)に使い方やできることは記載されています

## 開き方

みなさんも自分も Dev 環境などで、開いてみましょう

1. 設定のギアアイコンを押下する
2. 「開発者コンソール」と記載された箇所があるため押下する
3. 開発者コンソールが開かれる

---

# 開発者コンソールとは

![height:600](images/開発者コンソール_01.png)

---

# 開発者コンソールでできること

## Trailhead より抜粋

1. **Apex クラスやトリガー、Aura コンポーネント、Visualforce ページやコンポーネント**などに移動して開き、作成・編集する
2. 組織で作成したパッケージを参照する
3. **デバッグ用のログを生成して、さまざまな視点から分析**する
4. 自分の **Apex コードをテストして、エラーがないことを確認**する
5. Apex コードにチェックポイントを設定し、エラーを特定して解決する
6. 組織のレコードを**検索、作成、更新する SOQL と SOSL クエリを記述して実行**する

→ 開発は、開発者コンソールで**ほとんど**行うことができる
(※現代の開発環境からはかけ離れていますが...)

---

# Lightning Web Components と Aura の違いは？

- 相違点
  - Aura は開発者コンソールで作成・開発が可能だが、LWC は Visual Studio Code が必要([Chrome の拡張機能](https://chrome.google.com/webstore/detail/lightning-studio/ehkpneicmpbdejpoancidgkejlkahjgo?hl=ja)で代替品有)
  - LWC はユニットテスト[Jest](https://jestjs.io/ja/)に対応している
  - LWC で対応していない機能がまだある、その場合は Aura を使用する必要あり(一部モバイル対応など)
  - Aura は開発がアーカイブ化されている(サポートはしている)
    [Aura 開発リポジトリ](https://github.com/forcedotcom/aura)
    [LWC 開発リポジトリ](https://github.com/salesforce/lwc)

---

# Lightning Web Components と Aura の違いは？

- Visualforce との比較
  - 共通点
    - あまりない
  - 相違点
    - LWC の コントローラーは JavaScript(ブラウザ動作),Visualforce のコントローラーは Apex(サーバ動作)
      そのため、LWC のパフォーマンスが良い
    - モバイル上での対応が Aura と LWC の方が優れている

---

# Lightning Web Components と Aura の違いは？

- 画面フローとの比較
  - 画面フローで実装可能な場合画面フローを使用することが望ましい
  - ただ、ソースレビューを行いたい場合や、マージリクエストベース開発を行いたい場合は LWC の方がスムーズに行える
  - ブラウザの機能(localStorage など)を使用したい場合は LWC を使用することになる

---

# なぜ Lightning Web Components を選択するのか

- Aura
  - アーカイブ化されている(そのうちプロセスビルダーのように廃止されるかも？)
- Visualforce
  - コントローラーが Apex のためパフォーマンスが良くない
  - 利点はあるため、完全に必要ないわけではない
- Lightning Web Components
  - 消去法かつ Salesforce の推し機能なので LWC が良い
  - 他と比べると書きやすい(個人差あり)

---

# なぜ Lightning Web Components を選択するのか

- 開発コミュニティが活発なため、新機能などに期待できる
- 標準的な JavaScript を使用することができるため、JavaScript の開発経験がある方は開発しやすい
  - そのため、学習コストが低い & Web 開発を行う際に役立つかも？
- LWC 開発時に必要なファイルの数が少なく、初期段階の理解が早い(個人差あり)
- (Aura,Visualforce と比べると)パフォーマンスが良い
- ただ pdf の作成や classic で動作させたいなどの場合 Visalforce の方が優れている箇所もある
- Visualforce も Javascript は使用できるため、RemoteAction などを使用すれば LWC のように使用可能

---

# なぜ Lightning Web Components を選択するのか

- LWC で作成されるファイル数

```markdown
プロジェクト名(任意で設定可能)
├ HTML
├ JavaScript
├ xml
├ css(任意)
└ Jest フォルダ
　　 └ プロジェクト名.test.js
```

---

# なぜ Lightning Web Components を選択するのか

- Aura で作成されるファイル数
  - 全部が必要なわけではないが。。。

```markdown
プロジェクト名(任意で設定可能)
├ auradoc
├ cmp(HTML)
├ cmp-meta.xml
├ css
├ design
├ svg
├ Controller.js
├ Helper.js
└ Render.js
```

---

# なぜ Lightning Web Components を選択するのか

```html
<template>
  <div slds-p-left_xx-large>{hello}</div>
</template>
```

```JavaScript
import { LightningElement } from 'lwc';

export default class Test extends LightningElement {
  hello = 'Hello,World!'
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<LightningComponentBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>56.0</apiVersion>
    <isExposed>true</isExposed>
</LightningComponentBundle>
```

---

# LWC を使用した案件紹介

1. Experience Cloud に B to C と B to B 向けの Web ページを開発

- B to C のページは独自のデザインだったため、CSS を使用していた
- B to B の方は LDS だったが、ソースレビューや GitHub で管理を行いたかったため LWC で開発をおこなった

2. ルックアップ検索条件に表示されるレコードの条件を変更したい

- 画面フローでは実装不可だったため LWC を使用した
- その後、保存ボタンを動的に動かしたり、項目全て入力されたら保存ボタンの色を変えたりと色々した

---

# 作成した Lightning Web Components の紹介

- 勉強会の環境に一部デプロイします

---

# おまけ

- LWC は Salesforce の外でも使用することが可能
- [lwc.dev](https://lwc.dev/)という web ページがあり、こちらに詳細が記載されている
- Heroku や web サーバーにデプロイすることで使用可能
- メインの HTML と JavaScript の書き方はほぼ同じ
- 興味のある方は「OSS LWC」などで検索してみてください

---

# まとめ

- Aura と LWC の違いはさまざまあるが、基本 LWC を使用しよう
- 画面フローで実装可能な場合は、画面フローで実装しよう
