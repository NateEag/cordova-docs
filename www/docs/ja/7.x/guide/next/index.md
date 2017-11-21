---
license: >
    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.

title: 次のステップ
toc_title: Next Steps
---

# 次のステップ

コルドバ CLI を使用する方法を理解している開発者のためのプラグインを使用して、ビルドより良いよりパフォーマンスの高い Cordova アプリの横にある調査を考慮したいと思うことがありますいくつかのものがあります。 次のドキュメントはベスト ・ プラクティス、テスト、アップグレード、およびその他のトピックに関連するさまざまなトピックについてのアドバイスを提供していますが、規範的なものではありません。 このコルドバ開発者としてあなたの成長のためのあなたの起動ポイントを検討します。 また、改善することができます何かを見る場合は[貢献][1]してください。!

 [1]: http://cordova.apache.org/#contribute

このガイドには、次のトピックが含まれています。

*   ベスト ・ プラクティス
*   アップグレードの処理
*   Cordova アプリのテスト
*   Cordova アプリのデバッグ
*   ユーザー インターフェイス
*   特別な考慮事項
*   維持します。
*   ヘルプの取得 

# ベスト プラクティス Cordova アプリ開発

## 1） スパのお友達です。

何よりもまず - Cordova アプリはスパ (単一ページのアプリケーション） のデザインを採用すべきです。 広義では、スパは web ページの 1 つの要求から実行されているクライアント側アプリケーションです。 ユーザーがリソース (HTML、CSS、および JavaScript） の初期セットを読み込むし、さらに更新プログラム (データの読み込み、新しいビューを表示) は、AJAX を介して行われます。 スパは、一般的により複雑なクライアント側のアプリケーションに使用されます。 GMail は、これの素晴らしい例です。 GMail、メール ビュー、編集、および組織をロードした後は、完全に新しいものをロードするのではなく実際に現在のページを残して DOM を更新することによって行われます。

スパを使用して、効率的な方法でアプリケーションを整理するを助けることができるがまた Cordova アプリの特定の利点があります。 コルドバのアプリケーションは、deviceready 前にイベントを任意のプラグインを使用することがあります待つ必要があります。 Deviceready をする前に、再び起動するまで待機する必要があります、スパを使用しないでくださいあなたのユーザーが 1 つのページから別に移動するをクリックする場合は、プラグインの使用します。 これは、アプリケーションが大きくなるにつれて忘れられがちです。

コルドバを使用しないように選択した場合でも 1 つのページ アーキテクチャを使用しないモバイル アプリケーションを作成するだろう深刻なパフォーマンスへの影響 スクリプト、資産等を再読み込みする必要があるページ間を移動するためです。 これらの資産は、キャッシュされている場合でもパフォーマンスの問題がまだあるありますが。

Cordova アプリで使用することができますスパ ライブラリの例です：

*   [AngularJS][2]
*   [EmberJS][3]
*   [バックボーン][4]
*   [剣道 UI][5]
*   [モナカ][6]
*   [ReactJS][7]
*   [煎茶タッチ][8]
*   [jQuery Mobile][9]

 [2]: http://angularjs.org
 [3]: http://emberjs.com
 [4]: http://backbonejs.org
 [5]: http://www.telerik.com/kendo-ui
 [6]: http://monaca.mobi/en/
 [7]: http://facebook.github.io/react/
 [8]: http://www.sencha.com/products/touch/
 [9]: http://jquerymobile.com

さらに、多くは。

## 2） パフォーマンスに関する考慮事項

コルドバの新しい開発者が作ることができる最大の過ちの一つは、デスクトップ ・ マシンに取得パフォーマンスが同じモバイル デバイスになると仮定します。 私達のモバイル機器はより強力な毎年得ているが、彼らはまだパワーとデスクトップのパフォーマンスを欠いています。 モバイル デバイスは通常はるかに少ない RAM とは、自分のデスクトップからは程遠い GPU がある (またはノート) の兄弟。 ここでのヒントの完全なリストはあまりにも多くがここでは （さらなる研究の終わりに長いリソースの一覧) を心に留めていくつ。

**タッチとクリックして**- することができます最大かつ最も簡単な間違いは click イベントを使用します。 これら"作業中"だけで罰金携帯電話で、ほとんどのデバイスのタッチとタッチ「ホールド」イベントとを区別するためにそれらに 300 ms の遅延を課します。 使用して `touchstart` 、または `touchend` 、劇的な改善になります - 300 ms ような音は、多くがぎくしゃくの UI の更新と行動に結果することができます。 「タッチ」のイベントという事実はサポートされていませんをも考慮すべき非 webkit のブラウザーで[CanIUse][10]を参照してください。 これらの制限に対処するためにすることができますチェック アウト HandJS と Fastouch のような様々 なライブラリ。

 [10]: http://caniuse.com/#search=touch

**DOM 操作と CSS 切り替え**- ハードウェア加速 CSS 切り替えを使用してアニメーションを作成する java スクリプトの設定を使用するよりも劇的に良くなります。 例についてはこのセクションの最後にリソースの一覧を参照してください。

**ネットワークを吸う**- [ok]、ネットワーク常に吸うていない、モバイル ネットワークの待機時間がさらに良いのモバイル ネットワークは、おそらく考えているよりもはるかに悪い。 デスクトップ アプリ slurps 500 行の JSON データを 30 秒ごとを両方のバッテリーの豚と同様に、モバイル デバイスに低速になります。 Cordova アプリ （LocalStorage とたとえばファイル システム） アプリケーションでデータを保持する複数の方法があることに注意してください。 そのデータをローカル キャッシュであり、前後に送信しているデータの量を認識。 これは、アプリケーションが携帯電話ネットワークを介して接続されているときに特に重要な考慮事項です。

**追加のパフォーマンスの記事およびリソース**

*   ["あなたは半分中途半端それ」][11]
*   [「PhoneGap とハイブリッド アプリのトップ 10 のパフォーマンスのヒント」][12]
*   [「高速アプリ JavaScript のサイト」][13]

 [11]: http://sintaxi.com/you-half-assed-it
 [12]: http://coenraets.org/blog/2013/10/top-10-performance-techniques-for-phonegap-and-hybrid-apps-slides-available/
 [13]: https://channel9.msdn.com/Events/Build/2013/4-313

## 3） を認識し、オフライン ステータス処理

ネットワークについて前のヒントを参照してください。 だけでなく、低速のネットワークにすることができます完全にオフラインにすることがアプリケーションにとっては可能です。 アプリケーションは、インテリジェントな方法でこれを処理します。 アプリケーションない場合は、人々 は、アプリケーションが壊れていると思います。 易いというコルドバ サポート、オフラインとオンラインの両方のイベントをリッスンして） を処理するために、与えられた理由は全くない、アプリケーションをオフラインで実行されたときにも応答しないため。 (後述のテストを参照してください） をテストしてください、アプリケーション 1 つの状態で起動し、別に切り替えると、アプリケーションを処理する方法をテストしてください。

そのネットワーク接続 API だけでなく、オンライン イベントとオフライン イベント、完璧ではないに注意してください。 XHR 要求を使用して、デバイスが本当にオフラインまたはオンラインを参照してくださいするに依存する必要があります。 一日の終わりには必ず実際にネットワークの問題 - サポートのいくつかのフォームを追加、アップル ストア （とおそらく他の店） は、オンライン/オフライン状態を正しく処理しないアプリケーションを拒否します。 このトピックの詳細については、 [「この事ですか？」][14]を参照してください。

 [14]: http://blogs.telerik.com/appbuilder/posts/13-04-23/is-this-thing-on-%28part-1%29

# アップグレードの処理

## コルドバのプロジェクトをアップグレードします。

コルドバを使用して、既存のプロジェクトが作成された場合 3.x では、次を発行することによって、プロジェクトをアップグレードできます。

    コルドバ プラットフォーム更新プラットフォーム名 ios、アンドロイドなど。
    

コルドバのより前のバージョンの下で、既存のプロジェクトが作成されたかどうかは 3.x では、それがおそらく最適でしょう、新しいコルドバ 3.x プロジェクトを作成し、既存のプロジェクトのコードやアセットを新しいプロジェクトにコピーします。 一般的な手順は：

*   コルドバ 3.x のプロジェクトを新規作成 (コルドバ作成...)
*   Www フォルダー古いプロジェクトから新しいプロジェクトにコピーします。
*   古いプロジェクトから新しいプロジェクトに構成設定をコピーします。
*   古いプロジェクトを新しいプロジェクトで使用される任意のプラグインを追加します。
*   プロジェクトをビルドします。
*   テスト、テスト、テスト ！

プロジェクトの以前のバージョンに関係なくを読む、更新されたバージョンの変更点の更新コードを破る可能性があります絶対に重要です。 この情報を見つける最もよい場所はリポジトリとコルドバのブログに公開されたリリース ノートになります。 それが正しく動作する更新プログラムを実行した後を確認するためにアプリを徹底的にテストしたいと思う。

注: いくつかのプラグインはコルドバの新しいバージョンと互換性がない可能性があります。 プラグインに互換性がない場合、必要なものは、交換用プラグインを見つけることができる可能性があります。 または、プロジェクトのアップグレードを延期する必要があります。 また、プラグインを変更ために、それは新しいバージョンでは動作し、コミュニティに戻って貢献。

## プラグインのアップグレード

コルドバ 3.4 現在 1 つのコマンドを使用して変更されたプラグインをアップグレードするためのメカニズムはありません。代わりに、プラグインを削除し、プロジェクトに戻るし、新しいバージョンがインストールされているを追加します。

    コルドバ rm com.some.plugin コルドバ プラグイン追加 com.some.plugin
    

必ず更新済みプラグインのマニュアルを確認する、新しいバージョンで動作するようにコードを調整する必要があります。 また、プラグインの新しいバージョンは、コルドバのプロジェクトのバージョンで動作チェックを 2 倍します。

常に、新しいプラグインのインストールが壊れていない予想していなかった何かを確保するためにアプリをテストします。

プロジェクトに更新する必要があるプラグインの多く、それを削除し、1 つのコマンドでプラグインを追加シェルまたはバッチ スクリプトを作成する時間を節約可能性があります。

# Cordova アプリのテスト

アプリケーションをテストは超重要です。Cordova チームはジャスミンがすべて web フレンドリー ユニット テスト ソリューションを行います。

## 実際のデバイスで対シミュレータ上でテスト

コルドバのアプリケーションを開発するとき、デスクトップ ブラウザーおよびデバイス シミュレータ/エミュレーターを使用することも珍しくはないです。 ただし、可能な限り多くの物理デバイス上にアプリケーションをテストする非常に重要です：

*   シミュレータは、まさにそれ： シミュレータ。 たとえば、アプリは問題なく iOS のシミュレータで動作可能性がありますが、実際のデバイス (特に特定状況で、低いメモリの状態など） で失敗可能性があります。 または、実際のデバイスでうまく動作しながらシミュレータでアプリが実際に失敗します。 
*   エミュレーターは、まさにそれ： エミュレーター。 物理デバイス上のアプリケーションが実行どの程度とは関係ありません。 たとえば、いくつかのエミュレーターは、実際のデバイスには問題がありません、文字化けして表示とアプリをレンダリング可能性があります。 (この問題が発生した場合は無効に、エミュレーターでホスト GPU)
*   シミュレータは一般的に、物理デバイスよりも高速です。 その一方で、エミュレーターは一般的に遅くなります。 シミュレータやエミュレーターを実行する方法によっては、アプリのパフォーマンスを判断しないでください。 アプリのパフォーマンス スペクトルの実際のデバイス上で実行する方法を判断してください。
*   アプリが応答する方法あなたのタッチ、シミュレータやエミュレーターを使用しての良い感触を取得することはできません。 代わりに、実際のデバイスでアプリを実行して応答性などのユーザー インターフェイス要素のサイズとの問題を指すことができます。
*   プラットフォームごとの 1 つのデバイス上でのみをテストすることができるようにいいだろうが、多くの異なる OS バージョンのスポーツの多くのデバイス上でテストすることをお勧めします。 たとえば、何あなたの特定の Android スマート フォン上で動作可能性があります別の Android デバイスで失敗します。 IOS 6 端末で何 iOS 7 デバイス上で動作が失敗します。

それは、もちろん、市場で可能なあらゆるデバイス上でテストすることが可能です。 このため、さまざまなデバイスを持っている多くのテスターを募集することをお勧めします。 彼らはすべての問題をキャッチされません、チャンスが良い彼らが癖と単独で見つけることが問題を発見していることです。

ヒント: 簡単に Android のデバイス上の異なるバージョンをフラッシュするアンドロイドの Nexus デバイス上で可能です。 この単純なプロセスを簡単にお使いのデバイスを「脱獄」または「ルート」あなたを要求したりして保証排尿せず単一のデバイスに Android のさまざまなレベルでアプリケーションをテストすることができます。 Google の Android 工場イメージおよび指示は位置しています： https://developers.google.com/android/nexus/images#instructions

# Cordova アプリのデバッグ

コルドバのデバッグには、いくつかのセットアップが必要です。デスクトップ アプリケーションとは異なり単にオープン dev ツール、モバイル デバイス上にことはできませんし、デバッグを開始、幸いにもいくつかの素晴らしい選択肢です。

## iOS のデバッグ

### Xcode

Xcode Cordova アプリの iOS ネイティブ側をデバッグできます。 デバッグ領域は表示 (デバッグ領域->) を確認します。 アプリが実行されたらデバイス （またはシミュレータ） に、デバッグ領域でログ出力を表示できます。 これは、エラーや警告が印刷されます。 ソース ファイル内でブレークポイントを設定することもできます。 一度にコードの 1 行をステップし、その時点での変数の状態を表示することができます。 変数の状態はブレークポイントにヒットしたときにデバッグ領域に表示されます。 アプリが実行中で、デバイスで、一度を持ち出すことができます Safari の web インスペクター （後述） としてアプリケーションの webview および js 側をデバッグします。 詳細とヘルプは、Xcode ガイド参照してください： [Xcode デバッグ ガイド][15]

 [15]: https://developer.apple.com/library/mac/documentation/ToolsLanguages/Conceptual/Xcode_Overview/DebugYourApp/DebugYourApp.html#//apple_ref/doc/uid/TP40010215-CH18-SW1

### サファリでのリモート デバッグ Web インスペクター

Safari の web インスペクター コルドバ アプリケーションで webview および js のコードをデバッグできます。 これは OSX 上でのみ、iOS 6 (高い) でのみ動作します。 サファリを使用して、デバイス （またはシミュレータ） に接続しはコルドバ アプリケーションにブラウザーの dev ツールを接続します。 あなたは何を期待する dev ツール - DOM 検査/操作、JavaScript デバッガー、ネットワーク検査、コンソール、および得る。 Xcode のようなサファリの web インスペクターの JavaScript コードにブレークポイントを設定し、できますその時点での変数の状態を表示します。 任意のエラー、警告、またはメッセージをコンソールに出力を表示できます。 アプリが実行されているコンソールから直接 JavaScript コマンドを実行することもできます。 何を行うことができますを設定する方法の詳細については、この優れたブログの記事を参照してください： <http://moduscreate.com/enable-remote-web-inspector-in-ios-6/>とこのガイド： [Web インスペクターのサファリのガイド][16]

 [16]: https://developer.apple.com/library/safari/documentation/AppleApplications/Conceptual/Safari_Developer_Guide/Introduction/Introduction.html

## Chrome リモート デバッグ

Safari のバージョンとほぼ同じ、動作アンドロイドとだけが任意のデスクトップのオペレーティング システムから使用できます。 アンドロイド 4.4 (キットカット) の最小値、19、および （デスクトップ上で、30 + クロームの最小 API レベルが必要です。 一度接続すると、経験を得る、同じクロム Dev ツール、モバイル アプリケーション、デスクトップ アプリケーションと同様。 さらに、クロム Dev ツールいるミラー オプションをモバイル デバイスでアプリケーションを実行が表示されます。 これはちょうどより多くのビュー - スクロールし dev ツール] をクリックすることができ、モバイル デバイスで更新します。 Chrome リモート デバッグに関する詳細についてはここで見つけることがあります: <https://developers.google.com/chrome/mobile/docs/debugging>

WebKit のプロキシ経由の iOS アプリを検査するクロム Dev ツールを使用することが可能です: <https://github.com/google/ios-webkit-debug-proxy/>

## リップル

リップルはコルドバ プロジェクトのデスクトップ ベースのエミュレーターです。 本質的にそれができますコルドバ アプリケーション、デスクトップ アプリケーションで実行し、偽のコルドバのさまざまな機能。 たとえば、シェイク ・ イベントをテストする加速度計をシミュレートできます。 それはあなたのハード ドライブから画像を選択することによってカメラ API を偽物します。 リップル コルドバ プラグインを心配するのではなく、カスタム コードより集中することができます。 あなたがリップルについての詳細ここで見つけることができます： <http://ripple.incubator.apache.org/>

## Weinre

Weinre は、コルドバ アプリケーションのリモート デバッグ クライアントをホストするローカル サーバーを作成します。 インストールし、それを起動した後コルドバ アプリケーションにコードの行をコピーし、し再起動します。 その後、アプリケーションと共に動作するようにデスクトップ上 dev ツール パネルを開くことができます。 Weinre クロムほどおしゃれあり、サファリのリモート デバッグしますですが、オペレーティング システムとプラットフォームのはるかに広い範囲での作業の利点を持っています。 詳細についてはここで見つけることがあります: <http://people.apache.org/~pmuellr/weinre/docs/latest/>

## その他のオプション

*   ブラックベリー 10 と同様にデバッグをサポートします:[ドキュメント][17]
*   同様に Firefox アプリケーション マネージャーを使用してデバッグ、[このブログの記事][18]この[MDN の記事][19]を参照してくださいすることができます。.
*   例と上記のデバッグのヒントの説明を参照してください： <http://developer.telerik.com/featured/a-concise-guide-to-remote-debugging-on-ios-android-and-windows-phone/>

 [17]: https://developer.blackberry.com/html5/documentation/v2_0/debugging_using_web_inspector.html
 [18]: https://hacks.mozilla.org/2014/02/building-cordova-apps-for-firefox-os/
 [19]: https://developer.mozilla.org/en-US/Apps/Tools_and_frameworks/Cordova_support_for_Firefox_OS#Testing_and_debugging

# ユーザー インターフェイス

コルドバのアプリケーションを構築するは似合いますモバイルの挑戦、特に開発者のためすることができます。 多くの人々 は UI フレームワークを使用してこれを簡単にすることを選んだ。 ここでは考慮したい場合がありますオプションの短いリストです。

*   [jQuery Mobile][9] - jQuery Mobile は自動的にあなたのモバイルへの最適化のためのレイアウトを向上します。それも自動的にあなたのため、スパの作成を処理します。
*   [イオン][20]-この強力な UI フレームワークは、実際にプロジェクトの作成を処理する独自の CLI を持っています。 
*   [ラチェット][21]- ブートス トラップを作成した人々 によってもたらされます。 
*   [剣道 UI][5] - オープン ソース UI と Telerik からアプリケーション フレームワークです。
*   [トップコート][22]
*   [ReactJS][7]

 [20]: http://ionicframework.com/
 [21]: http://goratchet.com/
 [22]: http://topcoat.io

ユーザー インターフェイスを構築対象としているすべてのプラットフォームとユーザーの期待の違いについて考えることが重要です。 たとえば、iOS スタイル UI には、Android のアプリケーションはおそらく行かないもユーザーと。 これは、時も、さまざまなアプリケーション ストアによって強制されます。 このため、各プラットフォームの規則を尊重し、そのため様々 なヒューマン インターフェイス ガイドラインに精通していることが重要です。

*   [iOS][23]
*   [アンドロイド][24]
*   [Windows Phone][25]

 [23]: https://developer.apple.com/library/ios/documentation/userexperience/conceptual/MobileHIG/index.html
 [24]: https://developer.android.com/designWP8
 [25]: http://dev.windowsphone.com/en-us/design/library

## その他の UI の記事およびリソース

ブラウザー エンジンより多くの標準の苦情となって、我々 はまだ住んで接頭辞世界 (-webkit とさん)、次の資料が貴重なクロス ブラウザー アプリケーションでの UI のための開発: <http://blogs.windows.com/windows_phone/b/wpdev/archive/2012/11/15/adapting-your-webkit-optimized-site-for-internet-explorer-10.aspx>

# 特別な考慮事項

コルドバは、クロスプラット フォーム開発が容易になったが基になるネイティブ プラットフォームから 100 ％ の分離を提供することが可能ですだけではないです。だからことの制限に注意してください。

## プラットフォーム互換

マニュアルを読んで、さまざまな動作または複数プラットフォームでの要件の概要のセクションを探します。 存在する場合、これらは「iOS の癖」、等「Android 互換」というタイトルのセクションでされるでしょう。 これらの癖を読んで、コルドバで作業するには、それらに注意してください。

## リモート コンテンツの読み込み

リモートから読み込まれた HTML ページからコルドバの JavaScript 関数の呼び出し (「デバイスにローカルに格納されない HTML ページ) は、サポートされない構成です。 これはコルドバ意図していないこれは、Apache コルドバ コミュニティしませんこの構成のテストします。 いくつかの状況で動作することができます、しない推奨もサポートされています。 Java スクリプトの設定を維持する、同一生成元ポリシーと課題があり、コルドバのネイティブ部分同期バージョンでは、同じ (彼らが変更するプライベート Api を介して結合されている) ので、ネイティブのローカル関数および app ストアの潜在的な拒絶反応を呼び出すリモート コンテンツの信頼性。

リモートで読み込まれた HTML コンテンツは、webview の表示するべきコルドバの InAppBrowser を使用して。 InAppBrowser が実行されている JavaScript 上記理由のコルドバ JavaScript Api へのアクセスがあるないように設計されています。 『 セキュリティ [ガイド](../../index.html) 』 を参照してください。

# 維持します。

ここでは、コルドバで最新保つためにいくつかの方法です。

*   [コルドバのブログ][26]を購読します。.
*   [開発者メーリング リスト][27]を購読します。注 - これはサポート グループではありません!むしろこれは、コルドバの開発について議論する場所です。

 [26]: http://cordova.apache.org/#news
 [27]: http://cordova.apache.org/#mailing-list

# ヘルプの取得

次のリンクは、コルドバの助けを得る最もよい場所です。

*   StackOverflow: <http://stackoverflow.com/questions/tagged/cordova>コルドバのタグを使用して、表示およびすべてのコルドバの質問を参照できます。 StackOverflow によって、このようにことができます歴史的質問にアクセスするので「コルドバ」に「Phonegap」タグが自動的に変換されます
*   PhoneGap Google グループ: [https://groups.google.com/forum/#! フォーラム/phonegap][28]コルドバはまだ PhoneGap を呼び出されたとき、この Google グループは古いサポート フォーラム。 コルドバ コミュニティが代わりにサポートの StackOverflow を使用してこのグループにあまり焦点を当て関心を表明しているこのグループを頻繁にコルドバのユーザーの多くがまだ
*   ミート: <http://phonegap.meetup.com> - ローカル コルドバ/PhoneGap ミート グループを見つけることを検討

 [28]: https://groups.google.com/forum/#!forum/phonegap