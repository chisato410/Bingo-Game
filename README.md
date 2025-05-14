# 🎰 ビンゴマシーン

![screenshot](./screenshot.png) <!-- 任意: スクリーンショットを追加 -->

## 概要

HTML・CSS・JavaScript のみで構成された **ビンゴゲーム** です。授業の一環で制作し、DOM 操作、アニメーション、配列操作、イベント処理などの基本を活用しています。

---

## 🧩 機能一覧

- ランダム抽選機能（START/STOP）
- 番号の履歴を表示
- 自動的にビンゴ/リーチ判定
- カードの生成（NEW GAME）
- 点滅アニメーションによるリーチとビンゴ演出
- FREE マスの自動判定

---

## 📂 ファイル構成

```txt
bingo/
├── index.html         # 本体（HTML+CSS+JS一体型）
├── screenshot.png     # スクリーンショット画像
└── README.md          # このファイル
```

## 🚀 使い方

1. ブラウザで index.html を開く
2. 「NEW GAME」ボタンで新しいビンゴカードを生成
3. 「START」で数字がルーレットのように回転
4. 「STOP」で数字が確定され、カード上の該当マスが色付け
5. ビンゴ or リーチ時にはメッセージが表示される

## 🛠️ 技術ポイント

1. DOM 操作とイベントリスナー
   • querySelector() で HTML 要素を取得し、ボタンクリックなどのイベントを addEventListener で処理しています。
   • 動的にマスを生成し、class の追加・削除で状態を視覚的に表現しています。

2. 数字のシャッフル
   • Array.from() + Fisher–Yates シャッフル アルゴリズムを使用して 1〜75 の数字をランダム化。

```js
const shuffle = (array) => {
  for (let i = array.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [array[i], array[j]] = [array[j], array[i]];
  }
  return array;
};
```

3. ビンゴカードの生成
   • 5x5 のグリッドで 24 個のランダムな数字＋中央の「FREE」マスを表示します。
   • 中央の FREE マスは自動的に hit 判定に。

```js
card.splice(12, 0, "FREE");
```

4. リーチとビンゴの判定
   • 横 5 列、縦 5 列、斜め 2 列の 12 ラインを検査し、5 つすべて hit 状態ならビンゴ、4 つならリーチと判定します。

```js
const hitCount = line.filter((i) => cells[i].classList.contains("hit")).length;
```

5. アニメーションと演出
   • @keyframes を使ってビンゴラインが点滅したり、メッセージがポップアップしたりするような視覚効果を実装しています。

```css
@keyframes blink {
  0% {
    background-color: #ff6347;
  }
  100% {
    background-color: #ff0;
    color: #000;
  }
}
```

## 📚 学べたこと

    • JavaScript の配列操作
    • DOM の動的操作
    • クラスの操作による CSS 切り替え
    • イベント駆動の設計
    • CSS アニメーションの基礎
    • ゲームロジックの構築

## 🔧 今後改善したいこと

    •	ローカルストレージに記録を残す
    •	複数人でプレイ
    •	ビンゴ判定アルゴリズムの最適化
