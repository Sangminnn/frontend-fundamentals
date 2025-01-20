# 一緒に修正されるファイルは同じディレクトリに置く

<div style="margin-top: 16px">
<Badge type="info" text="凝集度" />
</div>

プロジェクトでコードを作成していると、Hook、コンポーネント、ユーティリティ関数などを複数のファイルに分けて管理することになります。こうしたファイルを簡単に作成、検索、削除できるように、適切なディレクトリ構造を確立することが重要です。

関連するソースファイルを同じディレクトリに配置することで、コードの依存関係を明確に示すことができます。これにより、参照してはいけないファイルを誤って参照するのを防ぎ、関連するファイルを一度に削除することも可能になります。

## 📝 コード例

次のコードは、プロジェクトのすべてのファイルをモジュールの種類（Presentational コンポーネント、Container コンポーネント、Hook、定数など）に応じて分類したディレクトリ構造です。

```text
└─ src
   ├─ components
   ├─ constants
   ├─ containers
   ├─ contexts
   ├─ remotes
   ├─ hooks
   ├─ utils
   └─ ...
```

## 👃 コードの不吉な臭いを嗅いでみる

### 凝集度

ファイルをこのように種類別に分けると、どのコードがどのコードを参照しているのかを簡単に確認できなくなります。コードファイル間の依存関係を開発者が自らコードを分析しながら把握する必要があります。
また、特定のコンポーネントや Hook、ユーティリティ関数が不要になり削除する場合、関連するコードが一緒に削除されずに残ってしまうこともあります。

プロジェクトの規模は時間とともに大きくなることが一般的で、プロジェクトのサイズが 2 倍、10 倍、100 倍と大きくなるにつれて、コード間の依存関係も同時に複雑になる可能性があります。1 つのディレクトリに 100 を超えるファイルが含まれることもあるでしょう。

## ✏️ リファクタリングしてみる

次のコードは、関連して修正されるコードファイルを一つのディレクトリにまとめるように構造を改善した例です。

```text
└─ src
   │  // プロジェクト全体で使われるコード
   ├─ components
   ├─ containers
   ├─ hooks
   ├─ utils
   ├─ ...
   │
   └─ domains
      │  // Domain1でのみ使われるコード
      ├─ Domain1
      │     ├─ components
      │     ├─ containers
      │     ├─ hooks
      │     ├─ utils
      │     └─ ...
      │
      │  // Domain2でのみ使われるコード
      └─ Domain2
            ├─ components
            ├─ containers
            ├─ hooks
            ├─ utils
            └─ ...
```

一緒に修正されるコードファイルを一つのディレクトリに配置すれば、コード間の依存関係を把握しやすくなります。

例えば、次のようにあるドメイン（`Domain1`）の下にあるコードで別のドメイン（`Domain2`）のソースコードを参照していると考えてみましょう。

```typescript
import { useFoo } '../../../Domain2/hooks/useFoo'
```

このような import 文に遭遇した場合、誤ったファイルを参照していることを容易に認識できるようになります。

また、特定の機能に関連するコードを削除する際に、1 つのディレクトリ全体を削除すれば、すべてのコードがきれいに削除されるため、プロジェクト内に不要なコードが残らないようにすることができます。