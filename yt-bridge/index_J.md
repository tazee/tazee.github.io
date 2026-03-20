---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
permalink: /yt-bridge/index_J.html
---

<style>
table {
  border-collapse: collapse;
  width: 100%;
}
table, th, td {
  border: 1px solid #ccc;
}
th, td {
  padding: 6px;
  text-align: left;
}
</style>

# YT-Bridge for Blender

- <a href="/yt-bridge/index.html">English document</a>

# 概要

YT-Bridge for Blender は BlenderとModoとの間でシーンデータを相互交換するためのツールです。メッシュデータだけでなく、ライトやカメラなどの情報も変換することができます。シーンデータを新しいバージョンのBlenderから古いバージョンのBlenderに変換する目的でも使用することができます。<br>

## Blenderのバージョンとインストール方法

- 4.0, 5.0以上、もしくはその派生バージョン
- アドオンはPythonのみで記述されており、macOS, Windowで動作します。

### Blenderアドオンのインストール

- Blender を起動します
- メニューから Edit > Preferences を開きます
- 左側の Add-ons を選択します
- Install from Disk をクリックして yt_bridge_blender.zip を選択します
- YT-Bridge のチェックボックスをオンにして有効にします

## Modoのバージョンとインストール方法

- Modo 16.1、Modo 17.1
- このキットはPythonのプラグインキットとして記述されており、macOS, Windowで動作します。

### Modoキットのインストール

- Modo を起動します
- yt_bridge_modo.zip をModoのビュー上にドラッグ＆ドロップします。
- Modoが再起動され、YT-Bridgeが使用可能になります。

### YT-Tools外部クリップボードとの違い

YT-Bridgeは、YT-Toolsの外部クリップボードの上位バージョンです。YT-Toolsの外部クリップボードがメッシュのポリゴンデータやその他の属性データを一時ファイル経由で変換するのに対し、YT-BridgeはBlenderのオブジェクト（Modoのアイテム）単位でデータを交換します。

|  | YT-Tools | YT-Bridge|
|---------|------------------|------------------|
| データ交換フォーマット | JSONテキスト | JSONテキスト・msgpackバイナリー |
| データ交換方法 | 一時ファイル・OSクリップボード | 一時ファイル |
| 名前を付けて保存・読み込み | _ | ○ |
| オブジェクト座標値 | ○ | ○ |
| Meshデータ | ○（*1） | ○ |
| Curveデータ | ○（*2） | ○ |
| Cameraデータ | _ | ○ |
| Lightデータ | _ | ○ |
| EMPTYデータ | _ | ○ |
| Armatureデータ | _ | ○ |
| リンクオブジェクト | _ | ○ |
| 読み込み選択オプション | _ | ○ |
| マテリアル上書きの可否 | ○ | ○ |
| 読み込み方法の指定 | ○（*3） | ○ |
| LightWaveとのデータ交換 | ○ | _ |

(*1) Custom Normalsは、サポートしていません（YT-Tools v1.8.2）<br>
(*2) Blender間でのコピー＆ペーストでのみ対応<br>
(*3) New Object from Clipboardとして新規オブジェクトにペースト<br>

## データ交換方法

YT-Tools外部クリップボードでは、中間データを交換する形式としてJSONテキストを使用しています。このJSONテキストデータの交換方法としては、一時ファイルおよびOSが提供するクリップボードをサポートしています。YT-Bridgeでは、中間データ形式をJSONテキストに加えて、よりファイルサイズがコンパクトなバイナリー形式をサポートしています。バイナリーデータは、Pythonのmsgpackを使って内部データをシリアライズしています。バイナリー形式のファイル入出力は一般的にテキスト形式よりも高速ですが、実際の入出力速度は使用する環境に依存します。YT-Bridgeでは、OS提供のクリップボードはサポートしていません。<br>

保存形式はパネルのフォーマットオプションで指定します。

## オブジェクトデータのプッシュ（書き出し）

YT-Bridgeのプッシュ操作は、YT-Toolsのコピーに相当し、指定した方法でオブジェクトデータを中間ファイルに保存します。

- All Objects (All Items)<br>
シーン内のサポートする全てのオブジェクトを書き出します。非表示のオブジェクトは出力されません。<br>

- All Objects (All Mesh Items)<br>
シーン内の全てのメッシュオブジェクトを書き出します。<br>

- Selected Objects (Selected Items)<br>
シーン内の選択されているオブジェクトを書き出します。<br>

- Selected Mesh Faces<br>
シーン内の選択されているメッシュオブジェクトの選択されているポリゴンだけを書き出します。なにも選択されていない場合、もしくはオブジェクトモードの場合は、全てのポリゴンが出力されます。<br>

## オブジェクトデータのプル（読み込み）

YT-Bridgeのプル操作は、YT-Toolsのペーストに相当し、中間ファイルに保存されているオブジェクトデータを指定した方法でシーンに読み込みます。

- New Objects (New Items)<br>
中間ファイルに保存されているデータを新規オブジェクトとして読み込みます。<br>

- Replace Objects (Replace Items)<br>
中間ファイルに保存されているオブジェクトデータを同一名称のシーン上のオブジェクトに上書きします。シーン上に一致する名称を持つオブジェクトがない場合は、新規オブジェクトに読み込みます。

- Duplicate and Replace Objects (Duplicate and Replace Items)<br>
Replace Objectsと同一ですが、オブジェクトデータの上書きを行う前に、その元オブジェクトの複製を作成します。複製したオブジェクトは非表示に設定されます。オブジェクトデータの上書きで作業を進めたいが、念の為元データのバックアップを作成しておきたい場合にこのモードを使用します。<br>

### オブジェクトタイプの選択

読み込みを行うオブジェクトのタイプをトグルボタンで指定します。Mesh、Curve、Light、Camera、Empty、Armatureが指定できます。

### Replace Materials

Replace Materialsを有効にすると中間ファイルに保存されているマテリアルデータで、シーン上のマテリアルデータを上書きします。読み込み先のマテリアルを優先させるには、このオプションをオフにしておく必要があります。

### Replace Object Transforms

Replace Object Transformsを有効にすると中間ファイルに保存されているオブジェクトの座標値で、シーン上のオブジェクト座標値データを上書きします。読み込み先のオブジェクト座標値データを優先させるには、このオプションをオフにしておく必要があります。

### Replace Modifiers

YT-Bridgeでは、Blenderのメッシュオブジェクトなどに設定されているモディファイア情報も中間ファイルに保存しています。Replace Modifiersを有効にすると中間ファイルに保存されているモディファイアのデータでシーン上のモディファイアを上書きます。モディファイアの上書きは、Blender間でのプッシュ・プル操作でのみ使用することができます。

### Import Custom Normals

Import Custom Normalsを有効にすると、中間ファイルに保存されているMeshオブジェクトのCustom Normalsを読み込みます。BlenderではCustom Normals、Modoでは頂点法線ベクトルマップに保存されます。

## 名前付きファイルへの保存・読み込み（Export/Import）

YT-Bridgeでは、中間ファイルを一時ファイルとしてOSが提供するフォルダに作成し、アプリケーション間でデータの交換を行っています。Export/Importではこのデータファイルをユーザーが指定したファイル名称で任意のフォルダに保存したり、読み込む機能を提供しています。

## データ変換詳細

### オブジェクト座標データ

BlenderのオブジェクトとModoのアイテム座標データは、位置座標値、回転座標値、スケール値、回転順序がそれぞれのローカル座標系で出力されれます。Blenderの座標系は右手座標系のZ-Up、Modoの座標系は右手座標系のY-Upです。座標値は中間データファイルから読み込む際に変換されます。また、オブジェクトのペアレンティングの情報も中間ファイルに保存されます。

### リンクオブジェクト（インスタンスアイテム）

Modoのインスタンスアイテムは、Blenderのリンクオブジェクトに相互に変換されます。Blenderのリンクオブジェクトは、シーン上で最初のリンクオブジェクトが実オブジェクトとして中間ファイルに保存され、それ以降のリンクオブジェクトがインスタンスとして出力されます。