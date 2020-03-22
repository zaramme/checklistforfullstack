# checklist_for_fullstack

日本のWeb開発業界で「フルスタックエンジニア」になるために必要な知識を、個人的経験からまとめました。

フルスタックエンジニアの定義ですが、ここでは、

- 企業で開発リーダー/テックリードとして、Web技術をベースとしたサービスの立ち上げからリリース、運用まで面倒を見られる。

というロールと仮定し、前提条件としては、どちらかというと立ち上げ直後のスタートアップや、社員数〜50位の小規模な組織を想定しています。
私がその分野に詳しい、というのもありますし、この規模を超えると、ある程度組織的な分業化が進むためフルスタックエンジニア、というポジションの必要性自体が薄まると考えています。ただ、大規模な組織であっても、テックリードと呼ばれるようなポジションの人は、ここで上げる項目については体系的な知識は求められるのではないでしょうか。

このチェックリストが埋まらないとフルスタックエンジニアになれない！かというと全くそんなことはなく、大抵のエンジニアは、実務を通して少しずつ埋めていくものであるし、何件も大規模なプロジェクトを経験しても、巡り合わせが悪くていまだに未経験な分野があったりもします。

ただ、技術者として１つのサービスを丸ごと作れる、と言えるようになりたいのであれば、今回挙げたような項目は、「逃げられない壁」として間違いなく立ちはだかります。事前の知識や勉強もそうですが、こうした側面があることをしっかりと認識した上で、果たすべき責任として着実に向き合っていくことこそが、フルスタックエンジニアとして必要なふるまいであると私は考えます。


## 1. 基本知識

### 技術の取得方法
- [ ] 業務の中で発生したエラーについて、自力で調べられる。
- [ ] 英語のドキュメントやブログ記事、Q&Aサイトを読むことができる。

### Linux
- [ ] CUI経由でSSHログインやファイル操作、パッケージやユーザー管理などの基本操作ができる。
- [ ] 必要に応じて、シェルスクリプトを使って作業を自動化したり、定期実行したりできる。
  - シェルスクリプトは描く頻度自体はさほど多くないので、ググりながら書ける、で十分だと思います。

### Git
- [ ] 自分が行うコミットに対して、必要な差分を行単位、コードブロック単位で調整できる。
- [ ] reset, rebase, revertなど、コミット改変系の操作を知っており、リポジトリで事故が起きた時に適切に対処できる。
- [ ] GitFlow or GithubFlowについて理解しており、プロジェクトに応じた必要なブランチ戦略を提案できる。

### プログラミング基礎
- [IPA 基本情報処理技術者試験](https://www.jitec.ipa.go.jp/1_13download/youkou_ver4_4.pdf) のテクノロジ系の内容は理解しておきたい。全然実務でも使います。
  - データベースとアルゴリズム
  - 論理演算(条件じゃない方のOR/AND, XOR)
  - n進数
  - 文字コード
  - TCP/IP
  - メモリアロケーションの仕組み
  - オーダー記法
  - などなど。実務でも意外と使います。



## 2.インフラ
- [ ] dockerを使って、プロジェクトに必要な仮想環境を１から構築し、チームで共有できる。
  - 単一コンテナではなく、DBやセッションなど、本番環境と同等のネットワーク構成をdocker-composeなどでオーケストレーションするものが望ましい

- [ ] クラウドインスタンス上で、Webサーバーを立ち上げるための手順書を作ることができる。
- [ ]本番/ステージング、開発環境のそれぞれの運用方針を定め、開発フェーズやフローに応じて各環境を運用・保守できる
- [ ] AWS or GCPを使って、システム開発に必要な構成を計画し、実際に構築することができる。(以下筆者がほとんどAWSなのでAWS主体で書きます)
  - ほぼ必須
    - IaaSインスタンス(EC2)は基本
    - DNS(Route s3) + ロードバランサー(ELB) + ネットワーク(VPC) でネットワーク構築
    - 特定機能についてのマネージド系サービス(RDS,S3,Redis)
  - 以下はどんなものか/何ができるか、メリットデメリットについて基礎知識があり、必要な時に調べて導入できればOK。
    - 監視やロギング（CloudWatchなど。何かしら必須ですが、実際の手法が多岐にわたるのでこの位置です）
    - コンテナの本番運用(ECSとかEKSとか)
    - リクエストキャッシュサーバー(CloudFlare)
    - サーバーレス構成(HerokuやFirebase Hostingとか、Webサーバーのアナロジー的に使うもの）
    - サーバーレス構成(AWS LambdaとかFirebase CloudFunctionのように、関数単位でより抽象化されたもの）
    - 検索特化DB(全文検索エンジンとかCloudSearchとか。NoSQLはDBセクションにあります)
    - mBaaS(Firebaseなど、モバイル特有の処理をシームレスに提供してくれる奴)
- [ ] CIツールを用いて、環境構築や最新コードのデプロイが自動化できる

## 3.バックエンド
- [ ] コンパイラ言語(Java, C#, Golangなど)、スクリプト言語(PHP,Ruby,Python)を最低限１つずつは使える。
  - 自分の得意言語に縛られず、各言語の特徴を踏まえた上でプロジェクトに導入できるのが望ましい
- [ ] MVCフレームワークについて精通しており、Webアプリケーションに頻出する機能について、適切に設計、実装できる。
  - ユーザー管理 / ログインセッションの管理
  - ルーティングの管理
  - ORM / マイグレーション
  - HTTPリクエスト処理(含むRest API)
  - バッチ処理(＝リクエストに依存しない定期実行処理やDB舐めるような重い処理)
  - HTMLテンプレート
  - 画像などのバイナリファイルやCSVなどのテキストファイルの読み書き
  - 外部ライブラリの導入およびパッケージ管理
  - 多分他にもたくさんある
- [ ] アプリケーションレイヤーの実行パフォーマンスに関して、数十秒〜数分かかるレベルの処理やメモリ展開量が多くなる可能性がある場合に、適切にチューニングができる
  - 大前提としてメモリ使用量が青天井にならないように
  - 実行時間がむやみにO(2^n)や、レコード数リニアにならないようにする
  - 大量データを処理する場合に、DBレイヤーで処理する部分とアプリケーションレイヤーで処理する部分を適切に切り分けられる

### 4.データベースレイヤー
- [ ] RDBの初期設定(ユーザー管理や設定ファイルとか)ができる
  - 有名RDBに関しては、ある程度PROS/CONSを知っていて、最適なものを検討、提案できるとよい(Amazon Aurora,MySQL,PostgreSQL。Oracle, SQL Serverはあまり使わないかもです）
- [ ] 処理実装に必要なDBクエリについて、ORMとの連携を前提として、SQL構文レベルでも理解している。
  - 集計系などの複雑なクエリに関しては、SQLで直接ゴリゴリ書けるのが望ましい
- [ ] 正規化やパフォーマンスを意識して、数十〜数百table位のデータベース設計ができる。
  - ユーザーのグループとロール、ハッシュタグ、履歴、版管理、動的カラム、月次集計など、ToCやToBでよくあるテーブル設計についてはある程度パターンとして知っておくと良い。
- [ ] データベース内部でのパフォーマンスチューニングや、Indexを用いた高速化ができる。
- [ ] インフラレベルでのパフォーマンスチューニングについて、代表的な手法についての知識があり、必要に応じて導入できる。
  - レプリケーション / シャーディング
  - 検索用中間テーブルとかカラムの平坦化とか
  - クエリキャッシュの導入
  - 特化型DBエンジン(インメモリDB, 全文検索, MongoDBとか)
  - クラウド上のマネージドDB(DynamoDB、ElasticSearch、CloudSearch)

### 5.フロントエンド
- [ ] HTML/CSSについて精通し、画面デザインやUI/UXについて、デザイナーと必要な実装の連携ができる。
  - 3ペイン構成、レスポンシブ対応、FloatやFlexboxを使った回り込みなどは、エンジニア側でも実装方法くらいは押さえておきたい。
  - SASSを始めとするメタ言語も必須に近いと思います。Web制作だとCompassとかGrunt, Bootstrapがまだ現役だったりするので、その辺りはデザイナー側に目線を合わせられた方がいいです。
  - デザイナーリソースが潤沢になくて、全画面のHTMLが上がってこないとか普通なので、ログイン画面くらいであればエンジニアが自前でさくっと小綺麗なな見た目の物を作った方がいいです。
- [ ] SEOおよびkeywordやOGPなどのメタ情報についての基礎知識を持ち、必要に応じて方針などをプロダクトオーナーや専門ポジの人と相談しながらサービスを運用できる
  - 具体的にどうすべきかはWebディレクターやSEOの専門家任せでも良いですが、検索流入やSNSシェアがどの程度重要になるのかは実装段階で意識して、ある程度の準備をしておかないとめちゃくちゃ手戻りが発生します。
- [ ] 生JavaScriptおよびjQueryについての理解
  - まだまだSPAが当たり前と言う程ではないので、jQueryをサクッと書いたりメンテする知識はあった方がいいです。
- npmを用いてパッケージ管理や、ビルドやトランスパイル環境、ビルトインサーバーなどのJS開発環境を構築できる
- [ ] フルスタックフレームワーク(React or Vue or Angular)について、最低1つはできるようにしたい
  - がっつりSPAとSPAじゃないパターンと両方を必要に応じて使い分けられるのが望ましいです。その意味ではフルスタック志向の人はVueの方が使い勝手がいいように思います。
  - SSRはまだまだ必須ではないと思います。流石にその辺まで来ると専任フロントエンドの出番な気がします。

### (ネイティブアプリ)
- 結論、Webベースのシステム開発であれば、ネイティブアプリを作れる、は必ずしも必須ではないと思っています
  - 私自身はiPhone(Swift)業務開発経験ありますが、プロジェクトを回す、という観点で言うと、開発における画面設計の重要度が高めだったり、ストア審査や端末でのユーザーテストなど観点でリリースまでのスケジュールや業務フローが天と地ほどの差があるため、両方に精通するのは相当しんどいと思っています。このあたりは私ができないから、と言うバイアスが含まれてしまっているかもです。すみません。
- [ ] Webベースのシステムと、ネイティブアプリの開発フローやライフサイクルの違いについて基本的な知識を持ち、将来的にネイティブアプリへの横展開が必要になる可能性や、その際に必要なAPI改修や、連携について、考慮した開発計画を立てることができる。
  - いわゆるWebViewベースであればこんな感じでいける、位の想定はしてもいいかもしれません。
  - NuxtのPWAあたりは、Web屋が手軽にモバイル環境に対応する手段としてはそれなりに有力になってきているように思うので、視野に入れておくといいかもしれません。

## 6.セキュリティと障害対応

- 大前提として、セキュリティに関してはエンジニアが最大当事者です。エンジニアの知識の抜け漏れは、そのままシステムの抜け漏れになるので、包括的な知識と実践が必要不可欠です。
- [ ]代表的な攻撃手法（XSS、SQLインジェクション、CORFなど）についての知識があり、定期的に情報を収集している。
  - とにもかくにも徳丸本を読むところから。

- [ ]サービスのインフラ構成全体に対して、セキュリティ方針と具体的な対応方針を計画し、運用することができる。
- 実装されるアプリケーションコードに対して、悪意のあるアクセスの可能性を常に考慮し、全体の方針と、個別コードのレビューの両面で常に対策をしながらプロジェクトを進めることができる。
- [ ]企業に求められる個人情報保護やプライバシーポリシーについて理解し、システム上のデータの取り扱いについて関係部署と適切に連携し、システムに反映できる。
  - Pマークの有無と、規約上のユーザーデータの取り扱い方針は実装前に確認した方がいいです。
- [ ]システムの可用性について理解し、プロジェクトの保守運用方針やトラブル対応について、適切に要件を定め、運用することができる。

## 7.マネジメント

- [ ]プロジェクトを以下の観点から、具体的な計画に落とし込み、実際に遂行することができる。
  - ビジネスサイドや、関連セクションとの要件のすり合わせ
  - 予算やスケジュール、チームメンバーの技術力やスキルセットに合わせた開発チームの立ち上げ
  - 計画〜リリースまでの具体的なスケジュールや、社内/社外リリース時期の見積もり、設定
  - 実装が完了した後の、QAやユーザーテスト、改善フェーズの計画、およびリリース基準の設定
- [ ]アジャイル開発をプロジェクトに導入し、プロジェクトで実践的に運用することができる知見と経験がある。
  - 型通りにスクラムの全プラクティスを回すと言うよりは、
    - １〜２週間のスプリントでどれくらい開発ができるか、を早い段階から可視化して、開発ペースを掴む
    - 成果物をベースにして、常に開発スコープやバックログを柔軟に変更、整理しながら進める
    - 上記をやりつつ、ちゃんと予定通りに開発が着地できるようにコントロールする
  - と言う感じで、実際に何件かプロジェクトをローンチしたり、あるいは失敗した経験があるといいです。
  - ウォーターフォールも背景知識としては押さえておきたいですが、Web開発だとしんどいと思います。そう言うのを求められたら、納期の前半分でかなり絞った必須機能をウォーターフォール開発して、残りの期間で改善フェーズと称してイテレーション回すとか、そういう手法をやります。
- [ ]システムの品質についてプロジェクトにとって適切な基準を、プロダクトオーナーと適切に議論して、決めることができる。
  - Webの場合、完璧なシステムとか無理もいいとこなので、「時間を書けてしっかりと担保したい部分」と「多少バグや不便なところがあっても少しずつ改善したほうがいい部分」について相互認識を取るのが基本だと思います。

- [ ] 「コード規約」「テストコード」「コードレビュー」「QA」「ユーザーテスト」などの手法を適切に組み合わせて、正式リリースに向けてシステムの品質を担保することができる。
  - 自動化テストばかり持て囃されますが、あらかじめユースケースを定めた受け入れテストや、多部署の人にランダムに使ってもらうユーザーテストも立派と言うか、実践的にはそっちの方がメインだと思います。
  - スタートアップだとQAエンジニアなんていないことが多いので、プロダクトオーナーやビジネスサイドのメンバーに「受け入れ基準作って」って投げることが多いです。ちゃんと作ってもらうにはエンジニアがちゃんと説明できないとあかんですが。
  - もちろん、トランザクション確認など、エンジニアが考えた方がいいテスト観点もあるので、うまく分担しましょう。


## 8.ビジネスサイド
- [ ]プロジェクトについて、ビジネスとして適切なコスト／スケジュール感覚を持つ。
  - エンジニア目線から考える「理想的な品質/開発フロー/チームでないと」はだいたいToo muchです。ちゃんと話し合って、妥協するところはしてください。エンジニアが頑固だと、ビジネスサイドの心理的安全性が下がります。
  - 私はスタートアップ特化なので、いわゆる資金調達金額に対してシステムコストがどれくらいかだったり、サービスローンチや収益化のタイミングまで意識して、スケジュールやチーム構成の計画を組みます。
- [ ]開発スコープに対して、ただ言われた通りに見積もるだけでなく、機能や要件のプライオリティに応じて、ベータ扱いでリリースを早めたり、一部オペレーションを簡略化する、といった段階的なリリース計画の提案ができる。

- [ ]営業活動についての適切なリテラシーを持つ。
  - 特にToBの場合は、完全リリースに先行して営業活動やデモの機会があったりするので、その辺りも意識できた方がいいです。
  - 業界特有のドメイン知識は当然あって、時にはシステム的な最適解と相反することもあります。その辺りも汲み取って解決できるくらいの経験と想像力は持っておきたい。

- [ ]CS業務に対してのリテラシーを持つ。
  - 業務システムなら当たり前ですが、ToCサービスであっても、運営側のオペレーションスタッフもユーザーの一人だと思ってください。管理画面のオペレーションとか画面構成を最適化するだけで、オペレーションコストがめちゃくちゃ減ったりもします。
  - システムは、業務オペレーションの一部にすぎません。特に初期フェーズでは、スプレッドシートの見込み管理とかデータ集計、ユーザーとの電話対応とか、アナログな部分はたくさんあります。そういった作業がどれくらいあるのか、あるいはシステムに取り込むべきなのか、という事についてもちゃんと考えて、提案ができるといいです。

- [ ]Webマーケティングについて、基本的な仕組みと、システムとの連携方法を理解している。
  - 特にキーワード広告に関しては、CVタグを貼り付けてアナリティクスと連携、みたいな部分で結構システム連携が必要になるので、押さえておくといいと覆います。

- [ ]メールマーケティングについて、基本的な仕組みと、システムとの連携方法を理解している。
  - 盲点になりがちなのが、システムからの自動メールとは別に、CSサイドからユーザーに一斉メールを送りたい、という場合であったり、そもそも顧客データベースがWebシステム外で管理される場合です。
  - MailChimpなどの外部サービスと連携して、しっかりと配信先、配信内容、効果測定ができるような仕組み化は、ToCのサービスであればだいたい必要になります。