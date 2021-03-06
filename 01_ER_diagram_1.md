# ER図1
## 全体
- テーブルに登録日, 更新日のカラムがない。
  > ActiveRecordでデフォルトで作られる登録日、更新日の記述もお願いいたします。もし持たないのであれば理由を教えてください。
- 管理者とエンドユーザー、商品が関連づけられている。
  > 管理者とエンドユーザー、商品を関連付けた理由はありますか？
- 受注明細テーブルがない。

## エンドユーザー
- 会員ステータスのカラムがない。
  > 顧客には退会手続き, 管理者には顧客のステータス（有効/退会）の切り替えが要件として定義されています。顧客が退会を行う際、データは見かけ上削除されますが、DBには残しておきたいため「論理削除」を使います。論理削除を使うことで、管理者は退会したユーザーの情報を閲覧することができます。現在のテーブルですと、論理削除を実行することができません。顧客にどのようなカラムを持たせますか？
- 配送先を複数保持することが出来ない。
  > 現在、ユーザーの登録住所以外に商品を配送することができません。配送先を複数保持できるようにしてください。

## 商品
- 入荷情報を保持できない。
  > 商品の入荷情報を保持できるようにしてください。
- 在庫数カラムが存在している。
  > 在庫数は入荷情報と受注履歴から算出することができます。商品に在庫数カラムを持たせてしまうと、「在庫数」と「入荷情報・受注履歴から算出される在庫数」の間に齟齬が生まれる可能性があります。
- 論理削除の機能が存在しない。
  > 商品を削除した場合にもその商品はDBに残しておきたいです。どのようなカラムを追加しますか？
- ディスクに対応して曲を管理できていない。
  > 1枚のディスクに対して曲が1曲とは限りません。曲を複数持つディスクをどのようにDBに登録しますか？
- アーティスト, レーベル, ジャンルそれぞれとのアソシエーションができていない。
  > 商品を登録する際、アーティスト、レーベル、ジャンルを直接手打ちで入力する仕様にすると、表記揺れが起こる可能性があります。事前に登録してあるデータから選択する設計が適切です。
- 発売日を保持するカラムがない。
  > 発売日を保持するカラムを作ってください。
- ステータスが何を意味しているか不明です。（）に意味を書くのではなくカラム名にわかりやすい命名をします。
  > 「ステータス」だけだと何のステータスを管理しているかが分かりません。具体的に命名してください。

## カート
- カート内商品を保持するため、テーブル名が適切でない。
  > 「カート」はユーザーが1つ持っているものです。本テーブルは「カートの中身」の情報を保持するものです。よって、「カートアイテム」などと命名するのが適切です。
- 外部キーである商品IDが機能していない。
  > 商品情報は外部キーを持たせることで引っ張ってくることが出来ます。
- エンドユーザーとカートを関連付けていない。
  > 現在、どのユーザーがどの商品をカートに入れているかが保持できません。ユーザーごとにカートアイテムは異なります。
- 合計金額カラムが存在している。
  > 本テーブルは、商品に関して「商品1つの情報」・「個数」を保持するため、合計金額を算出する必要はありません。合計金額カラムを持たせた理由を教えてください。
- PKの名前がテーブル名と合致していない。
  > PKが「注文id」になっています。テーブル名と対応させてください。

## 決済
- 受注情報を保持するためテーブル名が適切でない。
  > 決済だけでなく受注情報（配送先など）も保持します。よって受注テーブルなどと命名するのが適切です。
- 送料を保持するカラムがない。
  > 送料を保持するカラムを持たせてください。
- 請求総額を保持するカラムがない。
  > 請求総額の情報はどのように保持しますか。
- 購入日カラムがある。
  > 購入日は該当のレコードがDBに保存されたときです。よって、購入日は更新日と一致します。もし、更新日とは別に購入日カラムを追加した理由があれば教えてください。
- 宛名と郵便番号カラムがない。
  > 送付先住所の他に宛名、郵便番号を保持するカラムを追加してください。
- カートとのリレーションがある。
  > カートと本テーブルを関連づけた理由は何ですか？


<font color="Red">再提出の際はこのレビューを残しておいてください。</font>
##エンドユーザー
-会員ステータスのカラムがない。
>顧客には退会手続き, 管理者には顧客のステータス（有効/退会）の切り替えが要件として定義されています。顧客が退会を行う際、データは見かけ上削除されますが、DBには残しておきたいため「論理削除」を使います。論理削除を使うことで、管理者は退会したユーザーの情報を閲覧することができます。現在のテーブルですと、論理削除を実行することができません。顧客にどのようなカラムを持たせますか？
　→とても丁寧にレビューされているのですが、現状のレビューですと答えを言い過ぎてしまっているので、「論理削除」という言葉を使わずにレビューしてください。
　例：エンドユーザーが退会した場合、該当のレコードはどうなりますか？など

