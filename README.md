# KiCad Projects (Nixie Tube Boards)

趣味の電子工作として作成した KiCad 基板設計データをまとめたリポジトリです。  
主にニキシー管（IN-18等）に関連する駆動基板およびマウント基板の設計データを格納しています。

---

## 1. Projects Overview

### 1) IN-18_MountingBoard
手に入るもので最大のニキシー管 **IN-18** のマウント基板です。
* **特徴:** 下記の駆動基板（Driving Board）と同サイズで設計しており、スタックして（重ねて）使用することが可能です。
* **必要部品:**
    * ニキシー管 IN-18 ×2
    * ニキシー管用ソケットピン ×28
    * ピンヘッダ (2x6) ×2

### 2) NixieTube_DrivingBoard
ニキシー管用の汎用駆動基板です。
* **制御方式:** 外部マイコン（ESP32やArduino等）と **I2C** で接続。
* **仕組み:** GPIOエキスパンダ **MCP23018** で制御信号を生成し、ニキシー管専用ドライバ **K155ID1** (SN74141互換) に入力して各カソード（数字）を選択・点灯させます。
* **拡張性:** 電流制限抵抗値を調整することで、IN-18 以外の管にも流用可能です。コロン（ネオンランプ）制御用の回路（MPSA42使用）も搭載しています。

---

## 2. Hardware Specifications

| 項目 | 内容 |
| :--- | :--- |
| **Logic Voltage** | 5V (K155ID1の動作電圧) |
| **Anode Voltage** | DC 170V (ニキシー管駆動用高電圧) |
| **Communication** | I2C (Address はADRピンのジャンパ設定により変更可能) |
| **Driver IC** | K155ID1 (Russian Nixie Driver) ×2 |
| **Expander IC** | MCP23018 ×1 |

---

## 3. Bill of Materials (BOM)

### Driving Board 主要部品
* **ICs:**
    * MCP23018 (I/O Expander) ×1
    * K155ID1 (Nixie Driver) ×2
* **Discrete Components:**
    * MPSA42 (高耐圧トランジスタ：コロン制御用) ×4
    * ニキシー管用電流制限抵抗 ×2
    * 各種抵抗（BおよびBE抵抗、プルアップ等）
* **Connectors:**
    * ピンヘッダ (1x3) ×3
    * ジャンパピン ×3

---

## 4. Repository Structure
```text
.
├── IN-18_MountingBoard/       # IN-18マウント基板プロジェクト
│   ├── IN-18_MountingBoard.kicad_pro
│   └── ...
├── NixieTube_DrivingBoard/    # 駆動基板プロジェクト
│   ├── NixieTube_DrivingBoard.kicad_pro
│   └── ...
└── images/                    # 回路図・外観プレビュー画像（※適宜追加）