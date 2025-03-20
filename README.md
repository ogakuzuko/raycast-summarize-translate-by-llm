# HotKey AI Translator

Raycastアプリケーションで、選択したテキストをLLMを使用して要約・翻訳するツールです。

## 開発動機

- DeepLデスクトップアプリにある似た機能を多用していたがウィンドウが小さくて見辛いこと（普通にストレス）
- DeepLデスクトップアプリにある似た機能では、ライブラリコードのJSやPHPなどの複数行の英語コメントをアスタリスクまで含めて翻訳してしまい、翻訳がおかしくなってしまうのが地味にストレスだったこと
  - ![CleanShot 2025-03-19 at 23 52 40@2x](https://github.com/user-attachments/assets/91f13fe0-29b6-404a-8ce1-bf21160d931e)
- 長い文章を翻訳しようとするときにDeepLデスクトップアプリだと、翻訳が出るまでの時間が長く地味にストレスだったこと（全文翻訳できてからの表示だったのが大きな要因）
- DeepL Proに加入していて英文記事の全文翻訳をよく使っていたが、これからは全文翻訳とかじゃなくAIが記事を要約するのが主流になりそうだと思ったこと
- 月に何回も使っているわけでないDeepL Proの全文翻訳のために毎月1,000円ちょっと払う必要ないなと思ったこと

色々書いているけど、DeepLのショートカット起動にはめちゃくちゃお世話になっていたのでDeepLはとてもいいツール🐨

## Raycastにした理由

- DeepLデスクトップアプリ同様、Mac上に表示されるテキストならどこでも要約/翻訳できるようにしたかった点
  - ブラウザでは英文記事の翻訳によく使用していた。
  - その他Mac上のアプリケーションでは、特にIDEでライブラリのコードのコメントを翻訳するときや、ターミナルでのエラーメッセージなどの翻訳でよく使用していた。
- RaycastというMacアプリケーションの上に構築できるおかげで、本来なら必要なアクセシビリティの許可のフローが不要になる点
- ElectronでMacOS Appを作るのに比べて、Raycast上のストアに公開する方が手間が少ない点
- Raycast Ext.の開発にTypeScriptやReactが使用できる点

Raycast以外の他の候補として、MacOSアプリを作るElectronや、Chromeブラウザ拡張機能の案があったが、Chromeブラウザ拡張機能の案は要約/翻訳対象がブラウザ内のみに限定されてしまう点から除き、Electronの案はストア申請までの手間やインストール後のアクセシビリティの許可をユーザーに求める必要がある点（ユーザーが選択しているテキストの読み取りを実行するため）など、やりたいことの割に手間が多そうだったため、そのあとに思いついたRaycast App上に乗っかる方が、実行権限の手間などが既にクリアされていて、Electronのストア公開に比べてRaycast Ext.の公開の方が圧倒的に手間が省けることから、Raycastの拡張機能として作る方向でいくことに決めた。

## 開発前のLLM壁打ち

最初にChatGPTのDeep Researchを使って既存で似たようなものがないか探したが、あまりピンと来るものがなかったので、自分で作ろうと決めた。
その後、どういう方法で実現するのがいいかをClaudeと壁打ちして（特にClaudeである理由はなかった気がするがなんとなく）、そこでElectron案、ブラウザ拡張機能案が出たが、ふとRaycastも行けそうと思い立ってRaycast案についても聞いてみたところ、一番良さそうだったのでこの方向性で、再度ChatGPTに聞いたら、Raycast APIに`getSelectedText`というAPIがあることが分かり、実装方針が一旦見えたので、実装を始めることにした。

- ChatGPT
  - https://chatgpt.com/share/67d6f583-bfcc-8007-828f-2f7a1614efaf
- Claude
  - https://claude.ai/share/b76b64eb-3f61-4a59-8ce7-8adc40082baa

## 機能

- Mac上で選択したテキストを取得
- 選択したテキストをLLMに送信して要約・翻訳
- 結果をRaycast上にストリーミング表示

## 開発方法

```bash
# 開発サーバーの起動
npm run dev

# ビルド
npm run build
```

## 現在の進捗

- [x] 選択テキストの取得機能の実装
- [x] LLMとの連携
- [x] ストリーミング表示の実装
- [ ] UI/UXの改善
