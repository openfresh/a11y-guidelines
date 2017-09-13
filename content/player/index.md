---
layout: single
title: 視聴面のガイドライン
---

ユーザーが生放送を視聴する[視聴面](https://freshlive.tv)に関するガイドライン。<abbr title="Web Contents Accessibility Guidelines">WCAG</abbr>2.1がベースとなっている。

**※ガイドライン中のプログラムのコード例は、分かりやすさのため本来は必要な記述を省略していることがある。コード例をそのまま使用しないように注意すること。**

{{< wrapper >}}
<details>
<summary>目次</summary>
{{< outlineplayer >}}
</details>
{{< /wrapper >}}

### 1 知覚できる

コンテンツやUIをユーザーが知覚できる方法で提供する。

#### 1.1 代替テキスト

##### 1.1.1 画像に代替テキストを提供する

###### ガイドラインの意図

装飾ではないコンテンツとして画像には、その画像の代わりとなるテキスト（代替テキスト）を提供する。

- 視覚以外で情報を得ているユーザーへの情報提供
- 画像の配信、取得に失敗した際の代替コンテンツとして
- 画像検索などのサーチボットへのヒントとして

###### 実装方法 / 解説

**良くない実装**

`img` 要素に `alt` 属性が無い。

```html
<img src="fresh.jpg" />
```

意味のある画像を背景画像にしている。

```html
<div style="background-image: url(fresh.jpg)"></div>
```

**良い実装**

`img` 要素の `alt` 属性に代替するテキストを設定している。

```html
<img src="fresh.jpg" alt="FRESH!" />
```

**困った時**

<abbr title="Web Accessibility Initiative Accessible Rich Internet Applications">WAI-ARIA</abbr> の `aria-label` 属性を使用する。

```html
<div style="background-image: url(fresh.jpg)" aria-label="FRESH!" role="img"></div>
```

**解説**

- [`img` 要素には `alt` 属性で代替テキストを提供する](http://waic.jp/docs/WCAG-TECHS/H37)
- [非テキストコンテンツ:達成基準 1.1.1 を理解する | WCAG2.0解説書](http://waic.jp/docs/UNDERSTANDING-WCAG20/text-equiv-all.html)
- [altはつけるだけじゃなくて | 実践アクセシブルHTML 第一回](http://yuugop.com/articles/practicalaccessiblehtml/pah01.html)

※入力欄やボタンについては [3.3.2 入力欄のラベルまたは説明](#3-3-2-入力欄のラベルまたは説明) を参照のこと

###### テスト・チェック方法

1. ESlintによる自動チェック
  1. [eslint-plugin-jsx-a11y/accessible-emoji](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/accessible-emoji.md)
  2. [eslint-plugin-jsx-a11y/img-has-alt](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/img-has-alt.md)
  3. [eslint-plugin-jsx-a11y/iframe-has-title](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/iframe-has-title.md)
2. コードレビューによるチェック

#### 1.2 動画、音声に代替コンテンツを提供する

##### 1.2.1 収録済の音声及び動画に代替コンテンツを提供する

###### ガイドラインの意図

- 視覚的なコンテンツを見ることができない環境での利用やユーザーに役立つ
  - テキストデータが提供されていれば、音声や点字に変換することができる
  - 音声データが提供されていれば、代わりに情報を聴覚で得ることができる
- 音声が聞こえづらい、聞こえない、利用できない環境やユーザーでもコンテンツを理解することができる
  - スピーカーが壊れている、激しい騒音がある環境や静かな職場など聴覚障害を持つユーザーに限らない
- テキストデータで提供することにより、検索や流し読みができるようになり利便性が高まる

###### 実装方法 / 解説

**実装方法**

- 収録された音声のみのコンテンツには書き起こししたテキストを提供する
  - 話されている内容以外に、誰が話しているかも提供する
  - 話し言葉以外の情報、例えば喝采や笑い声についても起きている順番がわかるようにできる限りテキストにする
- 音声のない映像のみのコンテンツには、同等の情報を伝えるテキストや音声データを提供する
  - 音声データで提供する場合は、必ずしも合わせてテキストで提供する必要はない
  - 映像のすべてをテキストや音声にする必要はない
- 音声つき動画には、字幕（キャプション）、音声解説、もしくは書き起こしたテキストを提供する
  - 書き起こすテキストは、音声のみならず映像コンテンツの解説も含む（台本や脚本のイメージ）

代替コンテンツはコンテンツの前後に配置する、またはそれと分かる形でリンクするなどして提供する。

**例外**

ライブ配信のコンテンツ。ただし、可能な限り字幕の提供を行う。リアルタイムにテキストデータへと変換して提供することはコストがかかるが、聴き逃しした場合や環境の変化に強く、聴覚障害を持ったユーザー以外の利便性も高められる。

**解説**

- [時間依存メディアについて（カッコカリ） ::ハブろぐ](https://havelog.ayumusato.com/develop/a11y/e740-timed_base_media.html)
- [時間依存メディア:ガイドライン 1.2 を理解する | WCAG 2.0解説書](http://waic.jp/docs/UNDERSTANDING-WCAG20/media-equiv.html)

#### 1.3 様々な閲覧環境に適応できるようにする

情報、及び構造を損なうことなく、様々な方法で利用できるようにコンテンツを提供すること。

##### 1.3.1 情報及び関係性

コンテンツやUI、及びそれらの関係性をテキストで提供するか、プログラムによる解釈ができるようにする。

###### 実装方法 / 解説

**解説**

「プログラムによる解釈ができる」は、主にブラウザや検索エンジンなどのUA（ユーザーエージェント）が理解できるか、と考えて良い。

**実装**

適切な要素を用いてマークアップし、適切な属性を使用する。次に挙げるのは代表的な例で以下に限らない。

- [見出しを特定するために、h1 要素～ h6 要素を使用する](http://waic.jp/docs/WCAG-TECHS/H42.html)
- [リストは `ul` , `ol` , `dl` を用いる](http://waic.jp/docs/WCAG-TECHS/H48.html)
- [表の情報を提示するために、テーブルのマークアップを使用する](http://waic.jp/docs/WCAG-TECHS/H51.html)

###### テスト方法

- コードレビューによるチェック

###### 達成によるメリット

様々なデバイスやUAにコンテンツが正確に伝えられるようになる。

- スクリーンリーダー
- ブラウザのリーダーモード
- スマートウォッチなどのごく狭い画面のデバイス
- AppleのSiriや、AmazonのAlexaなど、スクリーンを持たない音声アシスタント
- 未知のデバイス

##### 1.3.2 意味のある順序

コンテンツの順番に意味がある場合は、正しく読む順番をプログラムが解釈できるようにする。

###### 実装方法 / 解説

1. [DOMの順番と表示順を一致させる](http://waic.jp/docs/WCAG-TECHS/C27)
2. [単語内の文字間を空けるためなど、文書の整形にスペースを利用](http://waic.jp/docs/WCAG-TECHS/F32.html)しない

解説 : [意味のある順序:達成基準 1.3.2 を理解する | WCAG 2.0解説書](http://waic.jp/docs/UNDERSTANDING-WCAG20/content-structure-separation-sequence.html)

###### テスト・チェック方法

- コードレビューによるチェック

##### 1.3.3 感覚的な特徴に依存しない

コンテンツやUIの説明は、色や形、視覚的な位置や方向、音などの感覚的な特徴だけで説明しない。

###### ガイドラインの意図

コンテンツやUIの説明が感覚的な特徴に依存すると、その感覚が使用できない場合や、コンテキストが変化した場合に利用が難しくなるため。

- 色や形などの視覚的特徴のみで説明した場合、視覚で情報を得られない環境やユーザーは利用できない
- 視覚的な位置や方向のみで説明した場合、レスポンシブデザインでレイアウトが変わった際に利用が困難になる

何より、明確なテキストラベルで対象を指示することは分かりやすさに繋がりすべてのユーザーにとって使いやすくなる。

###### 実装方法 / 解説

**良くない例**

視覚的な位置のみで説明している。

```
次に進むにはページ右下のボタンをクリックしてください
```

形のみで説明している。

```
OKなら丸いボタンをクリック、キャンセルは四角いボタンをクリックしてください
```

**良い例**

形や位置だけでなく、テキストによる説明も付け加える。

```
次に進むにはページ右下の「次へ」というボタンをクリックしてください。
```

```
OKなら丸いOKと書かれたボタンを、キャンセルは四角いキャンセルとかかれたボタンをクリックしてください
```

**解説**

- [UIやコンテンツについて形、または位置のみで特定](http://waic.jp/docs/WCAG-TECHS/F14)しない
- [UIやコンテンツについて指示、もしくは解説する文章にはUIのラベルテキストや機能についても言及する。](http://waic.jp/docs/WCAG-TECHS/G96)
- [感覚的な特徴:達成基準 1.3.3 を理解する | WCAG 2.0解説書](http://waic.jp/docs/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html)

###### テスト・チェック方法

- デザインレビューによるチェック

#### 1.4 判別できる

コンテンツを、ユーザーにとって見やすく聞きやすいものにすること。

##### 1.4.1 色だけで伝えない

色が、情報を伝える、動作を示す、反応を促す、又は視覚的な要素を判別するための唯一の視覚的手段としない。

###### 実装方法 / 解説

**良くない例**

色の違いだけで、必須項目やエラー項目を示す

```html
<label class="Label -required">電話番号
<input type="tel" required />
</label>
```

```css
.Label.-required {
  color: red;
}
```

```html
<p>20文字以上500文字以内で入力してください。</p>
<textarea></textarea>
<p><span class="NumCounter__Input -invalid">19</span>/500</p>
```

```css
.NumCounter__Input.-invalid {
  color: red;
}
```

**良い例**

色だけでなくテキストでも必須項目やエラーであることを示す。

```html
<label class="Label -required">電話番号（必須）
<input type="tel" required />
</label>
```

```html
<p>20文字以上500文字以内で入力してください。</p>
<textarea></textarea>
<p><span class="NumCounter__Input -invalid">19</span>/500</p>
<p>入力文字が不足しています。20文字以上入力してください。</p>
```

**解説**

- [色の違いで伝えている情報をテキストでも伝える](http://waic.jp/docs/WCAG-TECHS/G14)
- [色と模様、記号を併用する](http://waic.jp/docs/WCAG-TECHS/G111)
- [色の使用:達成基準 1.4.1 を理解する | WCAG 2.0解説書](http://waic.jp/docs/UNDERSTANDING-WCAG20/visual-audio-contrast-without-color.html)

###### テスト・チェック方法

- デザインレビューによるチェック

##### 1.4.2 音声を制御する

可能な限り音声を自動的に再生しない。音声が自動的に再生される場合は、音声を停止、またはコンテンツの音量を調整できるメカニズムを提供する。

1. [ユーザーが望む（と予想できる）際に限って音声を自動的に再生する](http://waic.jp/docs/WCAG-TECHS/G171)
2. 動画プレイヤーには音声の調整ボタン、ミュートボタンを搭載する

###### テスト・チェック方法

- 仕様策定段階での機能確認
- デザインレビューによるチェック

##### 1.4.3 コントラストを確保する

コンテンツやUI上のテキストやアイコンと背景に適切なコントラスト比を持たせる（4.5:1以上を推奨）。ただし、次の場合は除くが、可能な限りコントラスト比を確保する。

- 装飾的な文字、意味のない文字
- 操作不可能なUI上のテキスト
- ロゴタイプ
- コントラスト比が `3:1` 以上あり、かつ文字サイズが `18pt` 以上の場合

###### 実装方法 / 解説

**良くない例**

現在のFRESH!のカラースキームで推奨コントラスト比を満たしていないの組み合わせ。

{{< wrapper class="color-scheme" >}}

<dl>
<dt><code>--gray</code>と<code>--white</code>のコントラスト比は<em>2.7:1</em></dt>
<dd><p style="background-color: #9e9e9e;color: white;padding: 1em;">
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Nostrum voluptatum maxime voluptates quo aspernatur reiciendis, illo in tenetur. Minus odit aperiam ratione corporis nesciunt repellat cum vitae libero eius fuga!
</p></dd>
<dt>
<code>--gray-darkest</code>と<code>--blue</code>のコントラスト比は<em>4:1</em>
<small>※太字 or 大きな文字サイズであればOK</small>
</dt>
<dd><p style="background-color: #333;color: #1a9ebf;padding: 1em;">
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Mollitia aliquid incidunt fuga porro accusantium quaerat, doloremque autem magnam, aliquam fugit maiores. Aliquid a iste sapiente. Asperiores veniam placeat eaque, aperiam!</p>
</dd>
<dt>
<code>--white</code>と<code>--blue</code>のコントラスト比は<em>3.1:1</em>
<small>※太字 or 大きな文字サイズであればOK</small>
</dt>
<dd><p style="background-color: #fff;color: #1a9ebf;padding: 1em;border: 1px solid;">
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Illum, natus, odit. Dolor harum recusandae optio provident temporibus vero possimus quam itaque consequuntur, qui cum officiis at ducimus. Reiciendis quasi, temporibus.</p>
</dd>
<dt>
<code>--gray-deepest</code>と<code>--red</code>のコントラスト比は<em>4:1</em>
<small>※太字 or 大きな文字サイズであればOK</small>
</dt>
<dd><p style="background-color: #181818;color: #d9402b;padding: 1em;">
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Magnam obcaecati sint dicta sunt reprehenderit laudantium modi velit distinctio. Id facilis odio ipsum itaque vel saepe cumque iste ex, veniam obcaecati.</p>
</dd>
<dt>
<code>--gray-darker</code>と<code>--green</code>のコントラスト比は<em>3.7:1</em>
<small>※太字 or 大きな文字サイズであればOK</small>
</dt>
<dd><p style="background-color: #484848;color: #20bb75;padding: 1em;">
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eligendi aliquam aut nesciunt vitae sequi quas commodi eveniet debitis, fugiat laborum architecto illum, totam in! Nemo eum, sequi porro hic cumque.</p>
</dd>
</dl>

{{< /wrapper >}}

**最低限確保できているカラースキームの組み合わせ**

{{< wrapper class="color-scheme" >}}

<dl>
<dt><code>--gray-darker</code>と<code>--white</code>のコントラスト比は<em>9.1:1</em></dt>
<dd><p style="background-color: #484848;color: white;padding: 1em;margin-bottom: 2em;">
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Nostrum voluptatum maxime voluptates quo aspernatur reiciendis, illo in tenetur. Minus odit aperiam ratione corporis nesciunt repellat cum vitae libero eius fuga!
</p></dd>
<dt><code>--gray-deep</code>と<code>--blue</code>のコントラスト比は<em>4.6:1</em></dt>
<dd><p style="background-color: #2a2a2a;color: #1a9ebf;padding: 1em;margin-bottom: 2em;">
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Mollitia aliquid incidunt fuga porro accusantium quaerat, doloremque autem magnam, aliquam fugit maiores. Aliquid a iste sapiente. Asperiores veniam placeat eaque, aperiam!</p>
</dd>
<dt><code>--black</code>と<code>--red</code>のコントラスト比は<em>4.7:1</em></dt>
<dd><p style="background-color: #000;color: #d9402b;padding: 1em;margin-bottom: 2em;">
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Magnam obcaecati sint dicta sunt reprehenderit laudantium modi velit distinctio. Id facilis odio ipsum itaque vel saepe cumque iste ex, veniam obcaecati.</p></dd>
<dt><code>--white</code>と<code>--red</code>のコントラスト比は<em>4.5:1</em></dt>
<dd><p style="background-color: #fff;color: #d9402b;padding: 1em;margin-bottom: 2em;border: 1px solid;">
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Magnam obcaecati sint dicta sunt reprehenderit laudantium modi velit distinctio. Id facilis odio ipsum itaque vel saepe cumque iste ex, veniam obcaecati.</p></dd>
<dt><code>--gray-darkest</code>と<code>--green</code>のコントラスト比は<em>5.1:1</em></dt>
<dd><p style="background-color: #333;color: #20bb75;padding: 1em;margin-bottom: 2em;">
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eligendi aliquam aut nesciunt vitae sequi quas commodi eveniet debitis, fugiat laborum architecto illum, totam in! Nemo eum, sequi porro hic cumque.</p>
</dd>
</dl>

{{< /wrapper >}}

**解説**

- [コントラスト (最低限) : 達成基準 1.4.3 を理解する | WCAG 2.0解説書](http://waic.jp/docs/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html)

###### テスト・チェック方法

1. Sketch デザインデータをプラグインでチェックする
  - [Stark](https://github.com/stark-contrast/stark-sketch-plugin)
  - [Sketch-Color-Contrast-Analyser](https://github.com/getflourish/Sketch-Color-Contrast-Analyser)
2. デザインレビューによるチェック

※プラグインでは文字サイズと太字が考慮されないので注意する。

### 2 操作できる

UIコンポーネント及びナビゲーションは操作可能でなければならない。

#### 2.1 さまざまなデバイスでの操作

##### 2.1.1 キーボード、タッチデバイスでの操作

コンテンツやUIのすべての機能は、キーボードやタッチインタフェースで操作できるようにする。

###### 実装方法 / 解説

**良くない実装例**

フォーカスを受け取れない要素への `click` イベントの付与や `hover` 擬似クラスのみを利用したコンテンツの出し分けなど。

```html
<div onclick="...">
  content...
 </div>
```

**良い実装例**

フォーカスを受け取れる要素の使用、`tab-index`属性の付与、`focus` 擬似クラスの併用など。

```html
<button type="button" onclick="...">
   content...
</button>
```

[HTMLのフォームコントロール、及びリンクを使用する](http://waic.jp/docs/WCAG-TECHS/H91)

**解説**

マウスのみを想定しているUIでは、他のデバイスから使用できないことが多くあるが、キーボードやタッチデバイスでの操作を担保することで他のデバイスによる操作もカバーしやすくなる。

[キーボード : 達成基準 2.1.1 を理解する | WCAG 2.0解説書](http://waic.jp/docs/UNDERSTANDING-WCAG20/keyboard-operation-keyboard-operable.html)

###### 例外

- 手書き入力など、根本的な機能が始点から終点まで続く一連の軌跡に依存している機能

※ドラッグ&amp;ドロップ操作は軌跡に依存しないので、この例外には当てはまらない。

###### テスト・チェック方法

- ESlintによる自動チェック
  - [eslint-plugin-jsx-a11y/interactive-supports-focus](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/interactive-supports-focus.md)
  - [eslint-plugin-jsx-a11y/mouse-events-have-key-events](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/mouse-events-have-key-events.md)
- コードレビューによるチェック
- QAテスト（マウスと同じ操作がキーボードでできるかをテストする）

##### 2.1.2 シンプルな操作で操作できるようにする

コンテンツやUIのすべての機能は、複雑な操作に依存せずシンプルな操作で操作できるようにする。

###### 実装方法 / 解説

複雑な操作例 : 

1. 10秒以内に <kbd>↑</kbd><kbd>↑</kbd><kbd>↓</kbd><kbd>↓</kbd><kbd>←</kbd><kbd>→</kbd><kbd>←</kbd><kbd>→</kbd><kbd>a</kbd><kbd>b</kbd><kbd>a</kbd><kbd>b</kbd> を入力しないと出てこないメニュー
2. <kbd>→</kbd><kbd>↓</kbd><kbd>→+↓</kbd><kbd>p</kbd> を0.3秒以内に入力しないと出ない必殺技

###### 例外

デバッグモードへの移行など、ユーザーには秘匿した形で機能を提供する場合は例外とする。ただしその場合もチームメンバーの開発者の使用デバイスを考慮し慎重に行うこと。


##### 2.1.3 特定のデバイスの機能に依存しない

コンテンツやUIのすべての機能は、デバイスの特定の機能（タッチの圧力センサや、傾きセンサ）などに依存しなくても使用できるようにする。

###### 実装方法 / 解説

**良くない実装例**

iOS のフォースタッチでのみ動作するメニュー。

**良い実装**

他の操作方法に切り替える OR 代替の動作方法を提供する。

###### 例外

- VR（Virtual Reality）など、特定のデバイス専用に制作されているコンテンツ
- ペンの筆圧検知による線の太さの変更など、特定のデバイス専用の機能

##### 2.1.4 タッチターゲットサイズ

ポインティングのターゲットサイズは、タッチインタフェース向けUIでは 44×44 px以上を確保する。

###### 実装 / 解説

- ボタンUIやナビゲーションリンクに十分な余白を設ける

**解説**

タッチインタフェースにおいて、1つの指でタップするのにターゲットサイズが小さすぎると快適に操作できない。また視線入力デバイスなどのユーザービリティも向上する。

[ハーティーラダーでＷｅｂ閲覧 - YouTube](https://www.youtube.com/watch?v=g1iLTtjLD8E)

###### 例外

- 文章中のテキストリンク（※ただし、十分なフォントサイズを確保し、読みやすさだけでなく操作のしやすさも確保する）

###### テスト・チェック方法

- デザインレビューによるチェック
- コードレビューによるチェック

#### 2.2 十分な時間

ユーザーがコンテンツを読み、機能を使用するために十分な時間を提供すること。

##### 2.2.1 コンテンツの制限時間

コンテンツに制限時間を設けない。

###### 例外

- 制限時間があるコンテンツを利用する前に、制限時間を解除、又は初期設定の10倍以上の制限時間に変更することができる場合
- 時間切れとなる前に警告し、20秒前には簡単な操作で制限時間を延長することができる場合
- リアルタイムのイベント（ライブ配信中のアンケートやオークションなど）において、制限時間が必須の場合
- 制限時間が20時間よりも長い場合

###### 実装方法 / 解説

**解説**

自動更新するコンテンツ（ニュースティッカーやカルーセル）も、一種の制限時間付きのコンテンツと考えられる。

- [タイミング調整可能 : 達成基準 2.2.1 を理解する | WCAG 2.0解説書](http://waic.jp/docs/UNDERSTANDING-WCAG20/time-limits-required-behaviors.html)

##### 2.2.2 自動再生するコンテンツを一時停止、停止、非表示できるようにする

動きのあるコンテンツが自動的に開始され、また他のコンテンツと並行して表示される場合、ユーザーが一時停止、停止、または表示できないようにする。

###### 実装方法 / 解説

動きのあるコンテンツ = アニメーション、点滅、スクロール、コンテンツの自動更新も含む。

ウェブページの中に動作し続けるコンテンツがあると、その他のコンテンツの利用の妨げとなる。特に注意力欠如障害のユーザーなどはウェブページ全てを利用できない可能性がある。

###### 例外

- コンテンツの動作が5秒未満の場合
- 動き、又は自動更新がページ全体にとって必要不可欠な動作の一部である場合

#### 2.3 発作の防止

発作を引き起こすようなコンテンツを設計しないこと。

##### 2.3.1 フラッシュさせない

ウェブページには、1秒間に3回を超える閃光を放つものがない、又は閃光が一般閃光閾値及び赤色閃光閾値を下回っている。

###### 実装方法 / 解説

一般閃光閾値及び赤色閃光閾値 (general flash and red flash thresholds)

> あらゆる1秒間において、 一般閃光及び／又は赤色閃光 は3回以下である。もしくは、一般的な閲覧距離で、同時に生じている閃光が占める領域の合計が、画面上のどの視野10度においても、合計0.006ステラジアン (画面上の視野10度の25％) よりも多くを占めていない。
>
> ここで:
> 一般閃光とは、暗いほうの相対輝度が0.80未満であるときの、最大相対輝度の10%以上の相対輝度の交互の変化のことである。ここでいう「交互の変化」とは、増加した後に減少する、又は減少した後に増加するものを指す。そして、
> 赤色閃光とは、彩度の高い赤色を含んだ交互の遷移のことである。
> 例外: ホワイトノイズ又は1辺が (典型的な閲覧距離における視野の) 0.1度未満の市松模様のように、細かくて整っている模様の閃光は、閾値を超えることにはならない。

[3回の閃光、又は閾値以下:達成基準 2.3.1 を理解する](http://waic.jp/docs/UNDERSTANDING-WCAG20/seizure-does-not-violate.html)

#### 2.4 ナビゲーション

ユーザーがコンテンツを探し出したり、現在位置を確認したりする手助けをする。

##### 2.4.1 繰り返す情報のスキップ

複数のページ上で繰り返されている情報（ナビゲーションやサイトロゴなど）をスキップするメカニズムが利用できる。

###### 実装方法 / 解説

**解説**

必ずしもスキップリンクを設置する必要はなく、ウェブブラウザ標準の機能が利用できるように適切なマークアップを使用することで達成できる。マークアップによる達成方法は下記の通り。

- [ARIA11: ページの領域を特定するために ARIA ランドマークを使用する | WCAG 2.0 達成方法集](http://waic.jp/docs/WCAG-TECHS/ARIA11)
- [H69: コンテンツの各セクションの開始位置に見出し要素を提供する | WCAG 2.0 達成方法集](http://waic.jp/docs/WCAG-TECHS/H69)

**事例**

> ニュースを配信する組織のホームページには、広告、検索、その他のサービスのためのたくさんのブロック及びサイドバーに囲まれて、ページの中央にメインの記事がある。ページの先頭に、そのメインの記事へジャンプするリンクがある。このリンクを使わないと、キーボードを使用している利用者は、メインの記事へ到達するまでに Tab キーを押下しながら40前後のリンクを通り抜ける必要がある。また、スクリーンリーダーの利用者は、200の単語を聞かなければならない。そして、画面拡大ソフトの利用者は、メインの記事の場所を探し回らなければならなくなる。

[ブロックスキップ : 達成基準 2.4.1 を理解する | WCAG 2.0解説書](http://waic.jp/docs/UNDERSTANDING-WCAG20/navigation-mechanisms-skip.html#navigation-mechanisms-skip-examples-head)

##### 2.4.2 ページタイトル

ウェブページには、主題又は目的を説明したタイトルがある。

###### 実装方法 / 解説

HTMLの `<title>` 要素に、適切なタイトルを他のページと重複することなく記述すること。

[ページタイトル : 達成基準 2.4.2 を理解する | WCAG 2.0解説書](http://waic.jp/docs/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html)

### 3 理解できる

#### 3.1 読みやすさ

ユーザーや、ユーザーが使用するプログラムにとって理解しやすいような記述にする。

##### 3.1.1 ページの言語

それぞれのウェブページのデフォルトの自然言語がどの言語であるか、プログラムによる解釈が可能である。

###### 実装方法 / 解説

`<html>` 要素に `lang` 属性を記述する。

```html
<!DOCTYPE html>
<html lang="ja">
```

#### 3.2 予測できる

##### 3.2.1 ユーザーの意図しない変更をしない

ユーザーが予想できないタイミングでページ全体に及ぶような変更や現在地の移動を引き起こさない。

###### 例外

- 変更が起きることをユーザーへ事前に伝えている場合

###### 実装方法 / 解説

**解説**

ユーザーが予想できないタイミング = マウスホバーやキーボードフォーカスを当てるだけなど。

ホバーやキーボードフォーカスは、操作の前段階でありそのタイミングで重要な変化を引き起こすとユーザーが混乱してしまう。

**良くない実装例**

- フォーカスを受け取ったりマウスホバーすると自動的に送信されてしまうフォーム
- フォーカスを受け取ったりマウスホバーすると新しいウィンドウをひらかせるコンポーネント
- フォーカスを受け取ったりマウスホバーすると、ページ内の現在位置を移動したり別のページに移動したりさせるコンポーネント

**良い実装例**

クリックやエンターキーによる実行で変更を起こす。

#### 3.3 入力を支援する

##### 3.3.1 エラーの特定

入力エラーが自動的に検出された場合は、エラーとなっている箇所が特定され、そのエラーがユーザーにテキストで説明される。

###### 実装方法 / 解説

**良くない実装例**

スタイルのみでエラーであることを示し、エラーの内容が分からない。

```html
<label> ふりがな
<input type="text" class="Input -invalid" />
</label>
```

```css
.Input.-invalid {
	border: 2px solid red;
}
```

**良い実装例**

テキストでエラーの内容が明示されている。

```html
<label> ふりがな
<input type="text" class="Input -invalid" />
</label>
<p>ふりがなはひらがなかカタカナで入力してください</p>
```

※スタイルでも合わせて明示することを否定するものではない。

**解説**

- [エラーの特定 : 達成基準 3.3.1 を理解する | WCAG 2.0解説書](http://waic.jp/docs/UNDERSTANDING-WCAG20/minimize-error-identified.html)
- [ARIA21: Using Aria-Invalid to Indicate An Error Field | Techniques for WCAG 2.0](https://www.w3.org/TR/WCAG20-TECHS/ARIA21)

##### 3.3.2 入力欄のラベルまたは説明

ユーザーの入力を要求するUIには、ラベル又は説明文を提供する。

###### 実装方法 / 解説

**良くない実装方法**

`placeholder` 属性を入力内容の説明に使用する。

```html
<input type="text" placeholder="コメントを入力する" />
```

※ `placeholder` 属性での説明では入力が開始されると非表示になり、ユーザーを混乱させてしまう。

**良い実装方法**

近接する位置に説明を置き、 `label` 要素を用いて関連づける。

```html
<label> コメントを入力する
<input type="text" />
</label>
```

入力欄の隣に明確なラベルづけされたボタンを配置し、入力欄の説明とする。

```html
<input type="search" />
<button type="submit">検索</button>
```

説明と入力欄で構成されている節では、説明を見出しとし関連を可視化する。

```html
<section>
<h2>ご意見・ご要望</h2>
<form>
<textarea></textarea>
<button type="submit">送信する</button>
</form>
</section>
```

**解説**

- [ラベル又は説明 : 達成基準 3.3.2 を理解する | WCAG 2.0解説書](http://waic.jp/docs/UNDERSTANDING-WCAG20/minimize-error-cues.html)

### 4 堅牢性

コンテンツは、支援技術を含む様々なUAが確実に解釈できるよう十分に堅牢 (robust) でなければならない。

#### 4.1 互換性

未知のものを含む、さまざまなユーザーエージェントとの互換性を高めること。

##### 4.1.1 構文解析

HTML、及び構築するDOMは、要素には完全な開始タグ及び終了タグがあり、要素は仕様に準じて入れ子になっていて、要素には重複した属性がなく、どのIDも一意的にする。ただし、仕様で認められているものを除く。

[構文解析 : 達成基準 4.1.1 を理解する | WCAG 2.0解説書](http://waic.jp/docs/UNDERSTANDING-WCAG20/ensure-compat-parses.html)

##### 4.1.2 名前・役割、及び値

ユーザーが操作するすべてのUI（フォームを構成する要素、リンクなど）では、名前 (name) 及び役割 (role) は、プログラムによる解釈が可能である。又、状態、プロパティ、ユーザーが設定可能な値はプログラムによる設定が可能である。そして、支援技術を含むUAが、これらの項目に対する変更通知を利用できる。

###### 実装方法 / 解説

**良くない実装方法**

HTMLにある要素を利用せず、`<div>` や `<span>` を利用する。

```html
<span class="Button">button</span>
```

**良い実装例**

HTMLで定義されている要素を使用する。HTMLに適切な要素がない場合、WAI-ARIA で定義されている `role`属性で適切なものがあればそれを指定する。

```html
<button class="Button">button</button>
```

```html
<button role="tab" class="Tab">Tab</button>
```

**解説**

- [名前 (name) ・役割 (role) 及び値 (value) : 達成基準 4.1.2 を理解する | WCAG 2.0解説書](http://waic.jp/docs/UNDERSTANDING-WCAG20/ensure-compat-rsv.html)
- [5. The Roles Model : Accessible Rich Internet Applications (WAI-ARIA) 1.1](https://www.w3.org/TR/wai-aria-1.1/#roles)
