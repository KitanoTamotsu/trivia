## 　　Lesson16.　出力フォーマットへランダムにセットする  
#### 開発メモ

[サンプル動画](https://user-images.githubusercontent.com/40127279/126052259-d58e103a-5c2b-4e91-8d71-0ef8ef5f89c5.mp4)
ワークフロー
<br><img width="600" src="https://user-images.githubusercontent.com/40127279/127758662-62ca56a0-81c1-4eef-9c09-0cc66922957d.png">


### 1.HTMLをパースしない
　『トリビアの泉パーフェクトデータベース』を見つけた時に
<br>　Lesson14のRSSマニアライクなワークフローを作ろうと思い立ちました
<br>　ただ、この番組はもう終わっていて、トリビアの追加もないので
<br>　全てのトリビア1029個をスクリプトに埋め込みました
<br>　そう、おバカスクリプトです
<br>　文字列をスペース区切りで書いて、（）で括って、配列に格納しています
### 2.ランダムに9件を選んでAlfredフォーマットに出力する
　shufコマンドを利用します。ない方はインストールしてください
<br>　またインストール先をScriptFilterの先頭部分のPATHに定義してください
<br>（私はhomebrewでインストールしています）
<br>
<br>　shufコマンドはシャッフルの意味です
<br>　下記は0から1028までをシャッフルして先頭の9個をix配列に格納します
```
　ix=(`seq 0 1028| shuf| head -n 9`)
```
<br>　後は配列ixの要素を回してJSONをセットしています
<br>　※ver1.2でzsh化する際に1から1029に変更
<br>　
<br>　ScriptFilter（先頭部分）
<br>　<img width="600" src="https://user-images.githubusercontent.com/40127279/127758703-de1769c4-bf60-4ef5-9ac7-859e620768aa.png">
<br>　ScriptFilter（最後部分）
<br>　<img width="600" src="https://user-images.githubusercontent.com/40127279/127758706-b269b2df-7781-4def-855f-57c9615ca5c2.png">
#### 取扱説明
### 機能:
　トリビアの泉のランダム表示
<br>　元ネタは、[トリビアの泉パーフェクトデータベース](https://www.noncky.net/trivia/)から取得しました
### インストール:
　1.[Alfredworkflow](https://github.com/KitanoTamotsu/trivia/releases/download/1.2/trivia.alfredworkflow.zip)をダウンロード 
<br>　2.ファイルをダブルクリックしてワークフローに登録
### 使い方:
　キーワード『trivia』で起動
#### 修正履歴
### Ver1.1(2021-03-28)： 
・ScriptFilterのJSONフォーマットの編集をワンライナーから1行1プロパティーに変更

　修正前
 ```
　json=$json'{"title":"'${title[i]:0:24}'","subtitle":"'${hee[${ix[i]}]}'","arg":"'${link[i]}'"}'
 ```
 　修正後
 ```
  json=$json'{"title":"'${trivia[${ix[i]}]:0:24}'",'
  json=$json'"subtitle":"'${hee[${ix[i]}]}'",'
  json=$json'"arg":"'${trivia[${ix[i]}]}'"}' 
```
・ソースとは関係ありませんが、サンプル動画を投稿


ver1.2(2021-04-04)：
   シェルスクリプトをbashからzshに変更
<br>
<br>
[トップページに戻る](https://kitanotamotsu.github.io/)

