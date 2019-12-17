Discord_bot

### ソートなぞなぞ
***
　TLで見かけたソートなぞなぞ。楽しそうだったからBotを作ってみました。皆さんには非自明なソートの奇妙な面白さを味わってもらいます。
 
 #### ルール
 まず単語が与えられます。その単語を五十音順にソートしたものが与えられます。元になった単語を当ててください。
 
 例)　
 |未ソート |ソート済み|
 |:-:|:-:|
 |えつぴん|えんぴつ|
 |ペボルンー|ボールペン|
 
 ***
 #### 要件定義
 Discord bot　ソートなぞなぞ/sort riddle ”eddilr”
 - Python3を使用 
 - 出題中/問題受付の2つの状態を用意し、現在の状態をステータスに表示する
 - `/set`コマンドで解答を受け付けるチャンネルを現在のチャンネルに固定する
 - BotのDMに文字列を送信すると`答えキュー`にエンキューする。これを問題提出と呼ぶ
 - `答えキュー`の1つ目に対してソートを行い、`/set`されたチャンネルにソート済みの文字列を送信する。これを出題と呼ぶ
 - 出題された際にチャンネルが`/set`されていない場合は、`/set`を促すDMを出題した人に送信する
 - 問題受付中に問題提出されると出題中に遷移し、出題する
 - `/set`されたチャンネル内でbotにメンションしつつメッセージを送ることを解答と呼ぶ
 - 解答と`答えキュー`の1番目が一致している場合を正解と呼び、それ以外の場合を不正解と呼ぶ
 - 正解$\to$特定のメッセージを返し、`答えキュー`を１つデキューし、出題する。デキューできない場合は出題中から問題受付へ遷移する
 - 不正解$\to$何文字あってるかを返す
 - ギブアップ$\to$`答えキュー`の1つ目を表示し、`答えキュー`を１つデキューし、出題する。デキューできない場合は出題中から問題受付へ遷移する。コマンドは`/giveup`
 - `/clear`コマンドでキューを初期化する
 - `答えキュー`の上限は10(仮)とし、上限を超える問題提出は破棄し、その旨のメッセージを返す
 - 対応している文字列はひらがな、カタカナ、アルファベットの3種類。混在している場合は挙げた順番にソートされる