# 見積もり計算機


## 目的
- 個人として過去最長のプログラムの作成を目指し、ソフトウェア開発に挑戦しました。
- Pythonの習得を通じてプログラムに対する理解を深めることを目的としています。
- 現在在籍している会社での実用化を目指しています。

## 開発手順
1. 要件定義
2. 環境選定
3. コーディング

## 要件定義


#### フロントエンド
- 見積もりの作成（データ取得と全ての合計）
- 加工費の計算（データの保存と取得）

フロントエンドでは、ユーザーが効率的に作業できるように以下の機能を実装しました：
- ドラッグ&ドロップ機能のサポート
- 見やすいUIの設計と可能な限りの自動化
- 数値入力形式を基本とし、一部の項目はメニュー選択が可能
- 加工費計算のために専用の画面を設置

#### バックエンド
- 画像処理（テキストの取得、図形の取得、接戦の計算）

バックエンドでは、検出精度の向上を最優先とし、複数の画像処理機能を組み合わせて精度を高めています。

## 技術スタック
- **プログラミング言語**: Python
- **GUIライブラリ**: Tkinter
- **ウェブスクレイピング**: Selenium
- **画像処理**: pytesseract, pyocr, OpenCV (cv2)
- **データ保存形式**: JSONファイル
- **開発環境**: Visual Studio Code

## 環境選定
JavaScriptの経験を踏まえ、次のステップとしてPythonを学びたいという動機から環境を選定しました。また、複雑なロジックとデータ処理への関心からバックエンドの作成に挑戦しました。

- **GUI**: 軽量なTkinterを採用してリソース効率を考慮
- **ウェブスクレイピング**: 使用経験があり信頼性のあるSeleniumを採用
- **データ保存形式**: JavaScriptで扱い慣れていたJSONを選択

デバッグやテストのしやすさを考えた結果、Python、Tkinter、Seleniumの組み合わせが最適だと判断しました。

## 主な機能

### 材料費取得（スクレイピング）
![材料費１](https://github.com/user-attachments/assets/79528b99-2e8e-445e-879c-e760450485ac)
![材料費２](https://github.com/user-attachments/assets/19fc5a89-11b1-40d3-b8a1-3f75ea59543a)
- 幅・高さ・奥行きをmm単位で入力し、材料の右側にあるドロップダウンメニューから材料を選択,「材料費取得」ボタンを押すと、外部ウェブサイトから最新の材料費が自動的に取得され、計算フィールドに反映されます。
※著作権については、対象ウェブサイト側で非営利目的の利用が許可されていることを確認済みです。利用規約の変更に注意しながら、データの取得にはスクレイピングポリシーに従っています。

### 計算機（Tkinter）
![計算機１](https://github.com/user-attachments/assets/a89aec68-edff-4dc5-a012-2b8d35f9b9db)
![計算機２](https://github.com/user-attachments/assets/3ce4f26f-b9f3-4e7e-b91c-b6b852a4e24e)
![計算機３](https://github.com/user-attachments/assets/7856e1c2-fe72-4c0a-a613-ab9483c570a7)
- 加工コストの計算は別の画面で行います。見積もり画面の「加工コストの計算」ボタンを押すことで計算画面が立ち上がります。
- 加工計算画面で「加工名を追加」ボタンを押し、加工名と各パラメーターを入力可能です。
- 「計算」ボタンで合計値を出力し、「終了」ボタンで画面を閉じると、出力した合計値が見積もりの加工コストフィールドに反映されます。

### 画像処理
![画像処理１](https://github.com/user-attachments/assets/38b4af45-60c8-4c37-b43e-9a066a275766)
![画像処理２](https://github.com/user-attachments/assets/293d59d4-abba-433c-820d-4e8fa4b0197f)
![画像処理３](https://github.com/user-attachments/assets/350b9072-8a75-454b-8faa-641fc2e76823)
- 「画像読み込み」ボタンの横にあるフィールドに画像ファイル名を入力し、ボタンを押すと画像処理が開始され、結果がJSONファイルに保存されます。
- 検出にはcv2、pyocr、pytesseractの3つを使用し、精度の高い検出を実現しています。

## コーディング

### 見積もり
#### スクレイピング
- 選択した材料に応じて、Seleniumを使用して外部ウェブサイトから最新の材料費を自動取得します。

#### 加工コストの計算
- 加工コスト計算は別画面で行い、最終的な見積もりに組み込みます。

#### 画像認識機能
- OCR機能を統合し、画像からデータを読み取り手動入力を削減しています。

#### 加工費計算
- FrameとCanvasを用いてスクロール可能なインターフェースを実現しました。

#### ファイルのロードと保存
- ファイルからのデータ復元や、ファイル名を指定しての保存が可能です。
- コマンドライン引数に`chan`を指定することで、画像処理を行った場合は`chan == 1`になり、`orc_data.json`をロードし、ボタンの自動クリックが発動します。

### 画像処理
#### 主なプロセス
- 入力データを解析し、加工内容や精度、数量などのパラメータをJSON形式で保存します。
- 正規表現を用いてテキスト解析を行い、必要なパラメータを抽出しています。

#### 検索機能
- 図面からOCRでテキストを取得し、加工に関するキーワードのみを抽出します。

#### 接触判定
- cv2で図形の検出、pytesseractでテキスト位置情報を取得し、指定された図形に接している線やその線に接続する線を検出します。
- ベクトル計算を使って接触している線の位置や方向を解析し、加工対象の位置を特定しています。

#### スケールアップ処理・フィルタリング処理
- 通常サイズの画像で検出が難しい線などは、モノクロ度合いや画像サイズを調整して精度を向上させています。

#### JSON形式への保存
- 加工費計算に使用するJSONファイルを作成し、加工の種類や各パラメータを保存します。

## 改善点・今後の展望

### 課題と改善案

### 穴加工以外の取得
- 現在、画像処理で取得できる加工は穴加工に限られています。今後、他の加工にも対応するため、不要な線の除外や各加工に適したアルゴリズム導入を検討しています。

### 複雑な画像の処理
- テキストを円や線と誤認識することがあるため、テキストの位置情報を基に、その範囲を塗りつぶしてから図形検出を行う手順を検討しています。

### 作図機能
- OCRの接線描写機能を活用して、加工計算ソフトを転用し、入力値から図面を作成する機能を開発することが可能なため挑戦してみたいです。

### Webでの利用
- Webでの利用に挑戦したいと考えていますが、デプロイに関する知識を増やす必要があります。



