---
comments: false
---

# 変更しやすいコード

良いフロントエンドコードは **変更しやすい** コードです。
新しい仕様を実装する際に、既存のコードを修正してリリースのしやすいコードが良いコードだと言えます。
コードが変更しやすいかどうかは4つの基準で判断できます。

## 1. 可読性

**可読性**（Readability）は、コードがどれだけ読みやすいかを指します。コードを変更しやすくするためには、まずそのコードがどのように動くのかを理解する必要があります。読みやすいコードは、読む人が考えることを最小限に抑え、上から下へと自然に流れるように実装されています。

### 可読性を向上させる戦略

- **コンテキストを減らす**
  - [一緒に実行されないコードを分離する](./examples/submit-button.md)
  - [実装の詳細を抽象化する](./examples/login-start-page.md)
  - [ロジックの種類に応じて一体化している関数を分ける](./examples/use-page-state-readability.md)
- **名前付け**
  - [複雑な条件に名前を付ける](./examples/condition-name.md)
  - [マジックナンバーに名前を付ける](./examples/magic-number-readability.md)
- **上から下へ読めるようにする**
  - [視点の移動を減らす](./examples/user-policy.md)
  - [三項演算子をシンプルにする](./examples/ternary-operator.md)

## 2. 予測可能性

**予測可能性**(Predictability)とは、一緒に働くチームメンバーたちが関数やコンポーネントの挙動をどれだけ予測できるかを指します。
予測可能性が高いコードは、一貫したルールに従い、関数やコンポーネントの名前、パラメータ、返り値だけを見てもどのような挙動をするのかが分かります。

### 予測可能性を高める戦略

- [名前が被らないように管理する](./examples/http.md)
- [同じ種類の関数は返り値の型を統一する](./examples/use-user.md)
- [隠れたロジックを露呈させる](./examples/hidden-logic.md)

## 3. 凝集度

**凝集度**(Cohesion)とは、修正されるべきコードが常に一緒に修正されるかどうかを指します。凝集度が高いコードは、コードの一部を修正しても意図せず他の部分でエラーが発生しません。これは、一緒に修正されるべき部分が必ず一緒に修正されるようにコードが実装されているためです。

::: info 可読性と凝集度は相反することがあります

一般的に、凝集度を高めるためには変数や関数を抽象化するなど、可読性を低下させる決断をする必要があります。
一緒に修正されないとエラーが発生する可能性がある場合には、凝集度を優先してコードを共通化・抽象化してください。
リスクが高くない場合には、可読性を優先してコードの重複を許可してください。

:::

### 凝集度を高める戦略

- [一緒に修正されるファイルは同じディレクトリに置く](./examples/code-directory.md)
- [マジックナンバーを排除する](./examples/magic-number-cohesion.md)
- [フォームの凝集度について考える](./examples/form-fields.md)

## 4. 結合度

**結合度**(Coupling)とは、コードを修正したときの影響範囲を指します。コードを修正した際に影響範囲が小さく、変更に伴う影響を予測できるコードが、修正しやすいコードと言えます。

### 結合度を下げる戦略

- [責任を一つずつ管理する](./examples/use-page-state-coupling.md)
- [重複コードを許容する](./examples/use-bottom-sheet.md)
- [Props Drilling を解消する](./examples/item-edit-modal.md)

## コード品質を多角的に見る

残念ながら、この 4つの基準をすべて同時に満たすことは難しいです。

例えば、関数や変数を常に一緒に修正できるように共通化や抽象化を行うと、凝集度が高まります。しかし、その結果としてコードが一度抽象化されるため、可読性が低下します。

重複コードを許容することで、コードの影響範囲を減らし、結合度を下げることができますが、片方を修正した時にもう片方を誤って修正し忘れてしまう可能性があるため、凝集度が低下します。

フロントエンド開発者は、現在直面している状況を考慮し、よく考えた上で、長期的にコードの修正が容易になるにはどれを優先すべきかを検討する必要があります。