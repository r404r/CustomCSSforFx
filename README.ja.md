## 言語版

- [English](README.md)
- [简体中文](README.zh-CN.md)
- [日本語](README.ja.md)

## プレビュー

デフォルト状態:  
![デフォルトのプレビュー](assets/preview-001.png)

ツールバーにマウスオーバーした状態:  
![ツールバーのホバープレビュー](assets/preview-002.png)

## Firefox 向けダウンロード

- **[CustomCSSforFx - 現行リリースと更新履歴](https://github.com/Aris-t2/CustomCSSforFx/releases)** - **[102 ESR をサポートする最後のバージョン](https://github.com/Aris-t2/CustomCSSforFx/releases/tag/4.2.8)**  
- **[Firefox 用カスタム JavaScript スクリプト](https://github.com/Aris-t2/CustomJSforFx)** - **[NoiaButtons CSS 調整集](https://github.com/Aris-t2/NoiaButtons)**  


## ライセンス

このプロジェクトは GPLv3 と MPL 2.0 のデュアルライセンスです。詳細は LICENSE ファイルを参照してください。  


## 説明 / 使い方 / README

- [カスタム CSS を有効にする](#unlock-custom-css-usage)
- [WebExtensions では Firefox の外観を十分に変更できない理由](#webextensions-can-not-modify-firefox-appearance-properly)
- [Firefox のプロファイルフォルダーはどこ？ ユーザースタイルの正しい配置先](#where-to-find-firefox-profile-folder-the-correct-location-for-user-styles)  
- [カスタムユーザースタイルの使い方](#how-to-use-custom-user-styles)  
- [要素の id や属性を調べる方法](#how-to-find-item-ids-and-attributes)  
- [カスタム CSS コードをどこに追加するか](#where-to-add-custom-css-code)
- [カスタムユーザースタイルを編集する方法](#how-to-modify-custom-user-styles)  
- [Firefox Color（CustomCSSforFx のデフォルト配色プリセットと互換）](https://color.firefox.com/)    

<a id="unlock-custom-css-usage"></a>
## カスタム CSS を有効にする

`about:config` > `toolkit.legacyUserProfileCustomizations.stylesheets` > `true`  

<a id="webextensions-can-not-modify-firefox-appearance-properly"></a>
## WebExtensions では Firefox の外観を十分に変更できない理由

Firefox の UI を変更するには、ブラウザのプロファイルフォルダー内にある **userChrome.css** と **userContent.css** にカスタム CSS を追加する方法しかありません。  
また、CSS だけで新しい項目やボタン、ツールバーをゼロから作ることはできません。変更できるのは、すでに存在している UI 要素だけです。  

<a id="where-to-find-firefox-profile-folder-the-correct-location-for-user-styles"></a>
## Firefox のプロファイルフォルダーはどこ？ ユーザースタイルの正しい配置先

**1.** 自分のプロファイルフォルダーを探します（プロファイル名は環境ごとに異なります）。  
`about:support > プロファイルフォルダー > フォルダーを開く`  
または `about:profiles > ルートディレクトリー > フォルダーを開く`  

**2.** ユーザースタイルは `\chrome\` フォルダーに置きます。まだ存在しない場合は作成してください。作成後の構成は次のようになります。  
`\ PROFILE FOLDER NAME \chrome\`  

**3.** `userChrome.css`、`userContent.css`、および `\config\`、`\css\`、`\image\` フォルダーを `\chrome\` フォルダーへコピーします。配置後の構成は次のようになります。  
`\chrome\config\`  
`\chrome\css\`  
`\chrome\image\`  
`\chrome\userChrome.css`  
`\chrome\userContent.css`  

（任意）ディスク上のプロファイルフォルダーの場所:  
**Windows**  
`C:\Users\ USERNAME \AppData\Roaming\Mozilla\Firefox\Profiles\ PROFILE FOLDER NAME \`  
`AppData` フォルダーを見るには、隠しファイルを表示する必要があります。エクスプローラーのアドレスバーに `%APPDATA%\Mozilla\Firefox\Profiles\` を直接入力しても構いません。  
**Linux**  
`/home/ username /.mozilla/firefox/ profile folder name /`  
`.mozilla` フォルダーを見るには、隠しファイルを表示する必要があります。  
**Mac OS X**  
`~\Library\Mozilla\Firefox\Profiles\ PROFILE FOLDER NAME \` または  
`~\Library\Application Support\Mozilla\Firefox\Profiles\ PROFILE FOLDER NAME \`  
`\Users\ USERNAME \Library\Application\Support\Firefox\Profiles\`  

<a id="how-to-use-custom-user-styles"></a>
## カスタムユーザースタイルの使い方

_userChrome.css_ と _userContent.css_ は、オプション / 設定ファイルのような役割を持っています。主要な機能はここで有効化または無効化できます。  
_userChrome.css_ と _userContent.css_ を任意のテキストエディターで編集し（Windows では **[Notepad++](https://notepad-plus-plus.org/download/)** 推奨）、用意されている `@import` 行を変更、削除、またはコメントアウトすることで、使いたい機能を切り替えられます。  
変更を反映させるには、編集のたびに Firefox を再起動してください。  

**例**  
「ナビゲーションツールバーのボタンをクラシック風に表示」を<u>有効</u>にしたい場合、該当行は次のようにします。  
`@import "./css/buttons/buttons_on_navbar_classic_appearance.css"; /**/`  

「ナビゲーションツールバーのボタンをクラシック風に表示」を<u>無効</u>にしたい場合、該当行は次のようにします。  
`/* @import "./css/buttons/buttons_on_navbar_classic_appearance.css"; /**/`  

注記  
`/*` と `*/` の間にあるコードは、その間に別の `/*` や `*/` が入らない限り Firefox では読み込まれません。  

<a id="how-to-find-item-ids-and-attributes"></a>
## 要素の id や属性を調べる方法

次の設定は一度だけ有効にすれば十分です。  
1\. ツール > Web 開発 > ツールを切り替え > 「ツールをカスタマイズしてヘルプを表示」ボタン（三点ボタン）> 設定 > ブラウザー UI とアドオンのデバッグ用ツールボックスを有効にする  
2\. ツール > Web 開発 > ツールを切り替え > 「ツールをカスタマイズしてヘルプを表示」ボタン（三点ボタン）> 設定 > リモートデバッグを有効にする  

または、about:config で次の 2 項目を true に設定します。  

about:config > devtools.chrome.enabled > true  
about:config > devtools.debugger.remote-enabled > true  

`Ctrl+Alt+Shift+I` を押すか、「ツール > Web 開発 > ブラウザーツールボックス」を開きます。  

その後、UI や Web コンテンツを調査できます。  

ポップアップを検証中に開いたままにしたい場合:  
「ツールをカスタマイズしてヘルプを表示」ボタン（三点ボタン）をクリックし、「ポップアップの自動非表示を無効にする」を選択します。  

<a id="where-to-add-custom-css-code"></a>
## カスタム CSS コードをどこに追加するか

`userChrome.css` は末尾で `my_userChrome.css` をインポートしています（ファイルが存在する場合）。これは独自の CSS コード用に予約された場所です。

| 変更の種類 | 編集先 |
|-----------|-------|
| 既存機能モジュールの有効化/無効化 | `userChrome.css`（`@import` 行のコメントを切り替え） |
| 既存モジュールの変数値の調整（色やサイズなど） | 対応する `config/*.css` ファイル |
| プロジェクトに用意されていない新しいカスタムスタイル | `my_userChrome.css` |
| 既存モジュールのバグ修正 | 状況による: 小規模な修正は `my_userChrome.css`、大規模な変更はモジュールファイルを直接編集 |

`my_userChrome.css` は `userChrome.css` の最後にインポートされるため、読み込み優先度が最も高く、上方のすべてのモジュールのスタイルを上書きできます。さらに重要な点として、上游プロジェクトの更新時に `my_userChrome.css` は上書きされません。

<a id="how-to-modify-custom-user-styles"></a>
## カスタムユーザースタイルを編集する方法

CSS ファイルをテキストエディターで開き、コードを確認しながら必要な値に調整します。  
ファイルによっては、個別のケースに合わせて UI を微調整するための補足説明が含まれています。  
変更後は Firefox を再起動して反映させてください。  

_例_  
`./css/tabs/classic_squared_tabs.css` ファイルを開く  
`/* unloaded/pending tabs color *//*` を探す  
行末の `/*` を削除して、その部分のコードを有効にします。保存して Firefox を再起動してください。  

_例 2_  
`userChrome.css` ファイルを開く  
`@import "./css/tabs/classic_squared_tabs.css"; /**/` を探す  
行頭に `/*` を追加すると、「classic squared tabs」の外観を無効にできます。  
結果は `/* @import "./css/tabs/classic_squared_tabs.css"; /**/` のようになります。  
  
_例 3_  
`userChrome.css` ファイルを開く    
`/* @import "./css/locationbar/reader_alternative_icon.css"; /**/` を探す  
行頭の `/*` を削除すると、代替リーダーアイコンの外観を有効にできます。  
結果は `@import "./css/locationbar/reader_alternative_icon.css"; /**/` のようになります。  

## `chrome` フォルダーをシンボリックリンクで使う

CSS を頻繁に変更する場合、変更のたびに `current/` の内容を Firefox プロファイルへ手動でコピーする代わりに、プロファイル内の `chrome` フォルダーをこのリポジトリの `current/` フォルダーへ直接リンクすることもできます。

macOS や Linux では、シンボリックリンクで実現できます。

例:

```bash
ln -s "/path/to/CustomCSSforFx/current" "/path/to/Firefox/Profile/chrome"
```

この構成では、Firefox はリポジトリのチェックアウトから直接ファイルを読み込みます。
CSS を頻繁に調整する場合でも、再コピーは不要で Firefox を再起動するだけでよくなるため便利です。

注意:

- リンクを作成する前に、既存のプロファイル `chrome` フォルダーを削除するか名前を変更してください
- リンク先の `current/` フォルダーに `userChrome.css`、`userContent.css`、`config/`、`css/`、`image/` が含まれていることを確認してください
- 変更のたびに Firefox を再起動してください

Windows でも、ディレクトリシンボリックリンクや junction を使って、プロファイルの `chrome` フォルダーをリポジトリの `current/` フォルダーへ向ける構成は可能と思われますが、ここでは未検証です。
