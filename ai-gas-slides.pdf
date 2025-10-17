<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AIを味方につけよう！GASで業務自動化</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Meiryo', 'Noto Sans JP', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .slide-container {
            max-width: 1000px;
            margin: 0 auto;
            background: white;
            border-radius: 16px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.1);
            overflow: hidden;
            min-height: 700px;
            position: relative;
        }

        .slide-header {
            background: linear-gradient(90deg, #4285f4 25%, #ea4335 25% 50%, #fbbc04 50% 75%, #34a853 75%);
            height: 8px;
        }

        .slide {
            display: none;
            padding: 40px;
            min-height: 650px;
        }

        .slide.active {
            display: block;
        }

        .slide-title {
            font-size: 2.2rem;
            font-weight: 700;
            color: #4285f4;
            margin-bottom: 20px;
            line-height: 1.3;
        }

        .slide-subtitle {
            font-size: 1.4rem;
            color: #5f6368;
            margin-bottom: 30px;
            font-weight: 400;
        }

        .slide-content {
            font-size: 1.1rem;
            line-height: 1.6;
            color: #3c4043;
        }

        .instructor-info {
            position: absolute;
            bottom: 40px;
            left: 40px;
            font-size: 1rem;
            color: #5f6368;
        }

        .date-info {
            position: absolute;
            bottom: 40px;
            right: 40px;
            font-size: 1rem;
            color: #5f6368;
        }

        .bullet-list {
            list-style: none;
            margin: 20px 0;
        }

        .bullet-list li {
            margin: 12px 0;
            padding-left: 30px;
            position: relative;
            line-height: 1.5;
        }

        .bullet-list li::before {
            content: "●";
            position: absolute;
            left: 0;
            font-size: 1.2rem;
        }

        .blue-bullet::before { color: #4285f4; }
        .red-bullet::before { color: #ea4335; }
        .yellow-bullet::before { color: #fbbc04; }
        .green-bullet::before { color: #34a853; }

        .comparison-table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
            font-size: 0.95rem;
        }

        .comparison-table th,
        .comparison-table td {
            padding: 12px;
            text-align: left;
            border: 1px solid #dadce0;
        }

        .comparison-table th {
            background: #f8f9fa;
            font-weight: 600;
        }

        .code-block {
            background: #f8f9fa;
            border: 1px solid #dadce0;
            border-radius: 8px;
            padding: 20px;
            margin: 20px 0;
            font-family: 'Courier New', monospace;
            font-size: 0.9rem;
        }

        .navigation {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(0,0,0,0.8);
            border-radius: 25px;
            padding: 10px 20px;
            display: flex;
            align-items: center;
            gap: 15px;
            z-index: 1000;
        }

        .nav-btn {
            background: none;
            border: none;
            color: white;
            font-size: 1.5rem;
            cursor: pointer;
            padding: 5px;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .nav-btn:hover {
            background: rgba(255,255,255,0.2);
        }

        .slide-counter {
            color: white;
            font-weight: 500;
            min-width: 80px;
            text-align: center;
        }

        .highlight-box {
            background: #e8f0fe;
            border-left: 4px solid #4285f4;
            padding: 15px;
            margin: 20px 0;
            border-radius: 0 8px 8px 0;
        }

        .warning-box {
            background: #fef7e0;
            border-left: 4px solid #fbbc04;
            padding: 15px;
            margin: 20px 0;
            border-radius: 0 8px 8px 0;
        }

        .success-box {
            background: #e6f4ea;
            border-left: 4px solid #34a853;
            padding: 15px;
            margin: 20px 0;
            border-radius: 0 8px 8px 0;
        }

        .error-box {
            background: #fce8e6;
            border-left: 4px solid #ea4335;
            padding: 15px;
            margin: 20px 0;
            border-radius: 0 8px 8px 0;
        }

        .logo {
            position: absolute;
            top: 20px;
            right: 20px;
            font-size: 1.2rem;
            color: #5f6368;
        }

        .keywords {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            margin: 20px 0;
            border: 1px solid #e8eaed;
        }

        .keywords strong {
            color: #4285f4;
        }

        .two-column {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin: 20px 0;
        }

        .prompt-box {
            background: #fff3e0;
            border: 2px solid #ff9800;
            border-radius: 12px;
            padding: 20px;
            margin: 20px 0;
        }

        h3 {
            color: #4285f4;
            margin: 20px 0 10px 0;
            font-size: 1.3rem;
        }

        h4 {
            color: #ea4335;
            margin: 15px 0 8px 0;
            font-size: 1.1rem;
        }

        .example-box {
            background: #f0f4ff;
            border: 1px solid #c8d6ff;
            border-radius: 8px;
            padding: 15px;
            margin: 15px 0;
        }
    </style>
</head>
<body>
    <div class="slide-container">
        <div class="slide-header"></div>
        <div class="logo">Google Apps Script × AI</div>

        <!-- スライド1：タイトル -->
        <div class="slide active">
            <div style="text-align: center; margin-top: 80px;">
                <div class="slide-title">AIを味方につけよう！</div>
                <div class="slide-subtitle">Googleスプレッドシート×GASで<br>業務を自動化する魔法</div>
                <div style="margin-top: 40px; font-size: 1.2rem; color: #5f6368;">
                    AIに質問しながら、プログラミングと関数の基本を学ぶ
                </div>
            </div>
            <div class="instructor-info">講師名: 山本美優奈</div>
            <div class="date-info">2025年9月5日</div>
        </div>

        <!-- スライド2：導入 -->
        <div class="slide">
            <div class="slide-title">導入：なぜ、GASを学ぶのか？</div>
            
            <div class="keywords">
                <strong>キーワード：</strong>自動化、DX、効率化
            </div>

            <h3>GASとは？</h3>
            <p style="margin-bottom: 20px;">GoogleスプレッドシートやGmail、Googleフォームなど、Googleのサービス間を連携させるプログラミング言語です。JavaScriptをベースにしており、初心者でも比較的取り組みやすいのが特徴です。</p>

            <h3>具体例</h3>
            <ul class="bullet-list">
                <li class="blue-bullet">フォーム回答を自動でスプレッドシートに記録し、担当者に通知メールを送信</li>
                <li class="blue-bullet">毎日のデータを自動計算し、レポートを作成</li>
                <li class="blue-bullet">面倒な定型業務を代わりにやってくれるようになります</li>
            </ul>

            <div class="success-box">
                <strong>GASを使えば、面倒な作業から解放され、本来やるべき創造的な業務に集中できます！</strong>
            </div>
        </div>

        <!-- スライド3：本日のゴール -->
        <div class="slide">
            <div class="slide-title">本日のゴール</div>
            
            <ul class="bullet-list" style="margin-top: 40px;">
                <li class="blue-bullet">
                    <strong>AIと連携するスキルを身につける</strong><br>
                    AIに適切な質問をして、GASのスクリプトや関数を効率よく学ぶスキルを身につける
                </li>
                <li class="red-bullet">
                    <strong>技術の違いを理解する</strong><br>
                    GASとスプレッドシート関数の違いを理解し、適切に使い分けられるようにする
                </li>
                <li class="green-bullet">
                    <strong>問題解決力を高める</strong><br>
                    自分でエラーを解決したり、改善を積み重ねる問題解決力を身につける
                </li>
            </ul>

            <div class="warning-box" style="margin-top: 50px;">
                <strong>本日の学習は、プログラミング経験がなくても大丈夫！</strong><br>
                AIの力を借りて一緒に学んでいきましょう。
            </div>
        </div>

        <!-- スライド4：調べてみよう -->
        <div class="slide">
            <div class="slide-title">調べてみよう！AIと「GAS」と「関数」</div>
            
            <div style="margin: 30px 0;">
                <h3>みなさん、AIに質問してみましょう</h3>
                
                <div class="example-box">
                    <strong>ChatGPTやGeminiなどのAIを使って、GASと関数について質問してみましょう</strong>
                    <ul class="bullet-list" style="margin-top: 15px;">
                        <li class="blue-bullet">それぞれのツールで「何ができるのか」「どう使い分けているのか」を調べ</li>
                        <li class="blue-bullet">GASの利点やWebとの関係性について調べてみましょう</li>
                    </ul>
                </div>

                <h4>質問のヒントキーワード:</h4>
                <div class="code-block">
Google スプレッドシート 関数 違い
Google Apps Script 使い方
Google Apps Script メリット
GAS DX 関連
                </div>
            </div>

            <div class="warning-box">
                <strong>ポイント：</strong>あなたが調べた内容を元に、それぞれの特徴を比較表にまとめてみてください。
            </div>
        </div>

        <!-- スライド5：まとめ比較 -->
        <div class="slide">
            <div class="slide-title">まとめ：GASのメリットとDX推進</div>
            
            <p style="margin-bottom: 20px;">皆さんが調べた内容を元に、一緒に確認していきましょう。</p>

            <h3>GASの主なメリット</h3>
            <ul class="bullet-list">
                <li class="blue-bullet"><strong>手軽さ</strong><br>Googleアカウントがあればすぐに始められ、専用ソフトは原則必要ありません</li>
                <li class="red-bullet"><strong>連携性</strong><br>Googleのサービスと簡単に連携でき、様々な自動化が可能</li>
                <li class="green-bullet"><strong>コスト</strong><br>専用のツールと比べて大幅にコスト削減、個人でも利用可能</li>
            </ul>

            <h3>GASとDX推進の関連性</h3>
            <ul class="bullet-list">
                <li class="blue-bullet"><strong>「小さなDX」の実現</strong><br>大掛かりなシステム開発をせずとも、現場の担当者が自力で業務を自動化できる</li>
                <li class="red-bullet"><strong>効率化の入口</strong><br>普段の業務を効率化することで、従業員がより創造的な仕事に集中できるようになる</li>
                <li class="green-bullet"><strong>スキル開発</strong><br>プログラミングの基礎をつかみながら、UXマインドを身につけられる</li>
            </ul>
        </div>

        <!-- スライド6：調べてみよう！その2 -->
        <div class="slide">
            <div class="slide-title">調べてみよう！その2</div>
            
            <div style="margin: 40px 0;">
                <h3>今度は、GASと関数を比較してAIに質問してみましょう</h3>
                
                <div class="example-box">
                    関数とGASの違いを理解することで、それぞれを適切に使い分けられるようになります
                </div>

                <h4>質問のヒントワード:</h4>
                <div class="code-block">
Googleスプレッドシート 関数 GAS 違い
                </div>

                <h4>質問例を考える時間を設けます：</h4>
                <ul class="bullet-list">
                    <li class="green-bullet">何をするときに関数を使うべきか、どんな場面でGASが適しているか比較して下さい</li>
                </ul>
            </div>

            <div class="warning-box">
                <strong>ポイント：</strong>あなたが調べた内容を元に、それぞれの得意なことを比較表にまとめてみてください。
            </div>
        </div>

        <!-- スライド7：まとめ比較 -->
        <div class="slide">
            <div class="slide-title">まとめ：GAS vs 関数</div>
            
            <p style="margin-bottom: 20px;">ここからは、皆さんが調べた内容を元に一緒に確認していきましょう。</p>

            <div class="two-column">
                <div>
                    <h3>スプレッドシート関数</h3>
                    <ul class="bullet-list">
                        <li class="blue-bullet"><strong>計算</strong><br>データの処理・加工</li>
                        <li class="blue-bullet"><strong>整理</strong><br>データの並び替え・抽出・集計</li>
                        <li class="blue-bullet"><strong>セル内処理</strong><br>単一のセルシート内での処理</li>
                    </ul>
                </div>
                <div>
                    <h3>Google Apps Script</h3>
                    <ul class="bullet-list">
                        <li class="red-bullet"><strong>自動化</strong><br>繰り返し作業を効率的に実行</li>
                        <li class="red-bullet"><strong>連携</strong><br>Googleのサービス間でデータを連携</li>
                        <li class="red-bullet"><strong>トリガー</strong><br>時間やイベントに応じて実行</li>
                    </ul>
                </div>
            </div>

            <table class="comparison-table">
                <tr>
                    <th>項目</th>
                    <th>スプレッドシート関数</th>
                    <th>Google Apps Script (GAS)</th>
                </tr>
                <tr>
                    <td>主な目的</td>
                    <td>計算、データの整理</td>
                    <td>自動化、連携</td>
                </tr>
                <tr>
                    <td>処理範囲</td>
                    <td>セルやシート内</td>
                    <td>スプレッドシート全体、他のGoogleサービス</td>
                </tr>
                <tr>
                    <td>起動方法</td>
                    <td>セルへの入力</td>
                    <td>時間、イベント、手動実行</td>
                </tr>
            </table>

            <div class="success-box">
                <strong>GASと関数は競合するものではなく、組み合わせて使うことで、より強力な自動化システムが実現します</strong>
            </div>
        </div>

        <!-- スライド8：企業事例 -->
        <div class="slide">
            <div class="slide-title">企業での活用事例：GASはDXの強力なツール</div>
            
            <h3>なぜ、企業はGASを使うのでしょうか？特徴と人が求める効果を分析してみましょう</h3>

            <h4>事例1：人事・経理業務の自動化</h4>
            <ul class="bullet-list">
                <li class="blue-bullet"><strong>経費精算</strong><br>フォームで申請を受け付け、自動でスプレッドシートに記録し、承認者に通知</li>
                <li class="blue-bullet"><strong>勤怠管理</strong><br>スプレッドシートから給与データを集計し、給与システムと連携</li>
            </ul>

            <h4>事例2：マーケティング・営業活動の効率化</h4>
            <ul class="bullet-list">
                <li class="red-bullet"><strong>レポート作成</strong><br>Googleアナリティクスのデータを自動取得し、グラフとレポートを生成</li>
                <li class="red-bullet"><strong>顧客管理</strong><br>メイルフォームの回答をリストに自動登録し、セグメントに応じた対応</li>
            </ul>

            <div class="highlight-box">
                <strong>GASによるDX推進の成功要因</strong><br>
                <ul class="bullet-list">
                    <li class="green-bullet">専門知識のない現場社員が成し遂げ、大掛かりな組み込みなしに効率できる</li>
                    <li class="green-bullet">慣れれば短時間で効果が期待できる</li>
                    <li class="green-bullet">AIと組み合わせて、さらに高度な機能が向上に向上できる</li>
                </ul>
            </div>
        </div>

        <!-- スライド9：実践1 -->
        <div class="slide">
            <div class="slide-title">実践！AIと一緒にコーディング（1）</div>
            
            <h3>課題:</h3>
            <div class="highlight-box">
                「スプレッドシートのA1セルに『こんにちは！』と入力するGASを作成してください。」
            </div>

            <h3>AIへの質問:</h3>
            <div class="code-block">
GASでスプレッドシートのA1セルに「こんにちは！」と入力するコードを教えてください。
            </div>

            <h3>期待される回答例:</h3>
            <div class="code-block">
function myFunction() {
  // アクティブなスプレッドシートを取得
  var sheet = SpreadsheetApp.getActiveSheet();
  
  // A1セルに「こんにちは！」を入力
  sheet.getRange("A1").setValue("こんにちは！");
}
            </div>

            <div class="warning-box">
                <strong>ヒント：</strong>AIのコードをコピー&ペーストして、実行ボタンを押してみよう！
            </div>
        </div>

        <!-- スライド10：実践2 -->
        <div class="slide">
            <div class="slide-title">実践！AIと一緒にコーディング（2）</div>
            
            <h3>課題</h3>
            <div class="highlight-box">
                「GASで、A列に新しくデータが追加されたら、その行のB列に今日の日にちを自動で入力するコードを教えてください。」
            </div>

            <h3>AIへの質問:</h3>
            <div class="code-block">
GASでA列にデータが追加されたら、B列に日付を入れるコードを教えて。
            </div>

            <h3>ポイント：イベントドリブンの考え方</h3>
            <ul class="bullet-list">
                <li class="green-bullet"><strong>「イベントドリブン」とは</strong><br>特定の出来事（イベント）をきっかけに処理が行われる仕組みです</li>
                <li class="green-bullet"><strong>例</strong><br>フォーム送信、セル編集、時間経過などをトリガーとできます</li>
                <li class="green-bullet"><strong>利用例</strong><br>データ入力と、スプレッドシートの編集をきっかけにタイムスタンプで自動実行</li>
            </ul>

            <div class="warning-box">
                <strong>AIに質問する際は、具体的な状況を伝えるとより適切なコードが得られます！</strong>
            </div>
        </div>

        <!-- スライド11：困ったときは -->
        <div class="slide">
            <div class="slide-title">困ったときはAIに質問！</div>
            
            <h3>エラーの聞き方</h3>
            <ul class="bullet-list">
                <li class="red-bullet">エラーメッセージをそのまま伝えるのがコツ</li>
                <li class="red-bullet">どのような処理をしたときにエラーが起きたかも説明する</li>
            </ul>
            <div class="code-block" style="background: #fef7e0;">
ReferenceError: myFunction is not defined
            </div>
            <div class="success-box">
                <strong>「このエラーが出たのですが、どうすれば直せますか？」</strong>
            </div>

            <h3>コード作成の聞き方</h3>
            <ul class="bullet-list">
                <li class="green-bullet">何をしたいのかを具体的に伝える権威の基準</li>
                <li class="green-bullet">入力データと期待する結果を詳細に伝える</li>
            </ul>
            <div class="success-box">
                <strong>良い例：</strong>「GASで、スプレッドシートのA列の空いている空のセルを探して、そこに『完了』を入力するコードを教えてください。」
            </div>
            <div class="error-box">
                <strong>悪い例：</strong>「スプレッドシートのコードを教えてください」
            </div>

            <div class="warning-box">
                <strong>AIはコードの「理解」する強力なツールです。エラーの原因や解決法を詳しく説明してくれます！</strong>
            </div>
        </div>

        <!-- スライド12：まとめ -->
        <div class="slide">
            <div class="slide-title">本日のまとめ</div>
            
            <h3>GASの特徴</h3>
            <ul class="bullet-list">
                <li class="blue-bullet">自動化：繰り返し作業を効率的に処理業務を自動的に実行</li>
                <li class="blue-bullet">連携：Googleのサービス間でデータを連携する</li>
                <li class="blue-bullet">トリガー：時間やイベントに応じて仕組みを実行</li>
            </ul>

            <h3>関数の特徴</h3>
            <ul class="bullet-list">
                <li class="red-bullet">計算：数値データの処理・加工</li>
                <li class="red-bullet">整理：データの並び替え・抽出・集計</li>
                <li class="red-bullet">セル内処理：単一のセルシート内での処理</li>
            </ul>

            <h3>両者の関連性</h3>
            <ul class="bullet-list">
                <li class="green-bullet">協力関係：関数でできることはGASが補う</li>
                <li class="green-bullet">使い分け：単純な計算は関数、自動化はGAS</li>
                <li class="green-bullet">相互補完：両方を使いこなせればさらに効率的</li>
            </ul>

            <div class="highlight-box">
                <strong>AIの活用ポイント</strong><br>
                <strong>調べる</strong>：わからないことをすぐに調べ、経験を活用して深める<br>
                <strong>作る</strong>：コードを楽に作れちゃう。アイデアを形にする<br>
                <strong>直す</strong>：エラーの原因を早く、バグの修正方法を教えてもらう
            </div>
        </div>

        <!-- スライド13：応用編 -->
        <div class="slide">
            <div class="slide-title">応用編：AIに相談してみよう！</div>
            
            <h3>究極のプロンプト:</h3>
            <div class="prompt-box">
                あなたは、GASとGoogleスプレッドシートの専門家です。私は、新しいタスクをスプレッドシートに入力すると、自動でカレンダーに登録し、担当者にリマインダーメールを送るシステムを作りたいです。この目的を達成するための、GASと関数の具体的な役割分担を教えてください。また、今後このシステムを改善するためのアドバイスもお願いします。
            </div>

            <div class="success-box">
                <strong>AIは、あなたの頼れるパートナーになります。</strong><br>
                複雑なシステムも段階的に構築できるよう、AIがサポートしてくれます。
            </div>
        </div>

        <!-- スライド14：最後に -->
        <div class="slide">
            <div class="slide-title">最後に</div>
            
            <div style="margin: 50px 0; font-size: 1.2rem; line-height: 1.8;">
                <p>今日の授業で学んだスキルは、DXが求められる現代において、仕事や日々のタスクを効率化する上で非常に役立ちます。</p>
                
                <p style="margin-top: 30px;">これからも、AIを上手に活用して、たくさんのことを自動化し、あなたの時間を有効に使ってください。</p>
                
                <div class="highlight-box" style="margin-top: 40px;">
                    <strong>今後の学習のヒント：</strong><br>
                    小さな自動化から始めて、徐々に複雑なシステムへと発展させていきましょう。<br>
                    AIは常にあなたの学習パートナーとして活用できます。
                </div>
            </div>
        </div>

        <!-- スライド15：終了 -->
        <div class="slide">
            <div style="text-align: center; margin-top: 200px;">
                <div class="slide-title" style="font-size: 3rem;">ありがとうございました。</div>
                <div style="margin-top: 30px; font-size: 1.3rem; color: #5f6368;">
                    GASでの開発も楽しんでみてね
                </div>
            </div>
        </div>
    </div>

    <div class="navigation">
        <button class="nav-btn" id="prevBtn">‹</button>
        <span class="slide-counter"><span id="currentSlide">1</span>/15</span>
        <button class="nav-btn" id="nextBtn">›</button>
    </div>

    <script>
        let currentSlideIndex = 0;
        const slides = document.querySelectorAll('.slide');
        const totalSlides = slides.length;

        function showSlide(index) {
            slides.forEach(slide => slide.classList.remove('active'));
            slides[index].classList.add('active');
            document.getElementById('currentSlide').textContent = index + 1;
        }

        function nextSlide() {
            currentSlideIndex = (currentSlideIndex + 1) % totalSlides;
            showSlide(currentSlideIndex);
        }

        function prevSlide() {
            currentSlideIndex = (currentSlideIndex - 1 + totalSlides) % totalSlides;
            showSlide(currentSlideIndex);
        }

        document.getElementById('nextBtn').addEventListener('click', nextSlide);
        document.getElementById('prevBtn').addEventListener('click', prevSlide);

        // キーボードナビゲーション
        document.addEventListener('keydown', (e) => {
            if (e.key === 'ArrowRight' || e.key === ' ') {
                nextSlide();
            } else if (e.key === 'ArrowLeft') {
                prevSlide();
            }
        });

        // 初期表示
        showSlide(0);
    </script>
</body>
</html>
