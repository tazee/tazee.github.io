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
- Modoの初期設定でPythonのバージョンを3.9に設定してください。
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
| Meshデータ | ○ | ○ |
| Curveデータ | ○（*1） | ○ |
| Cameraデータ | _ | ○ |
| Lightデータ | _ | ○ |
| EMPTYデータ | _ | ○ |
| Armatureデータ | _ | ○ |
| StaticMeshデータ | _ | ○ (*2)|
| リンクオブジェクト | _ | ○ |
| Transformアニメーション | _ | ○ |
| 読み込み選択オプション | _ | ○ |
| マテリアル上書きの可否 | ○ | ○ |
| 読み込み方法の指定 | ○（*3） | ○ |
| LightWaveとのデータ交換 | ○ | _ |

(*1) Blender間でのコピー＆ペーストでのみ対応<br>
(*2) ModoのStaticMeshをMeshオブジェクトに変換して出力<br>
(*3) New Object from Clipboardとして新規オブジェクトにペースト<br>

## データ交換方法

YT-Tools外部クリップボードでは、中間データを交換する形式としてJSONテキストを使用しています。このJSONテキストデータの交換方法としては、一時ファイルおよびOSが提供するクリップボードをサポートしています。YT-Bridgeでは、中間データ形式をJSONテキストに加えて、よりファイルサイズがコンパクトなバイナリー形式をサポートしています。バイナリーデータは、Pythonのmsgpackを使って内部データをシリアライズしています。バイナリー形式のファイル入出力は一般的にテキスト形式よりも高速ですが、実際の入出力速度は使用する環境に依存します。YT-Bridgeでは、OS提供のクリップボードはサポートしていません。<br>

保存形式はパネルのフォーマットオプションで指定します。

## オブジェクトデータのプッシュ（書き出し）

YT-Bridgeのプッシュ操作は、YT-Toolsのコピーに相当し、指定した方法でオブジェクトデータを中間ファイルに保存します。中間ファイルのデータは読み込み先のアプリケーションから手動でプル操作を行う必要があります。YT-Bridgeではアプリケーション間通信を使用した自動読み込み機能は提供していません。

- All Objects (All Items)<br>
シーン内のサポートする全てのオブジェクトを書き出します。非表示のオブジェクトは出力されません。<br>

- All Objects (All Mesh Items)<br>
シーン内の全てのメッシュオブジェクトを書き出します。<br>

- Selected Objects (Selected Items)<br>
シーン内の選択されているオブジェクトを書き出します。<br>

- Selected Mesh Faces<br>
シーン内の選択されているメッシュオブジェクトの選択されているポリゴンだけを書き出します。なにも選択されていない場合、もしくはオブジェクトモードの場合は、全てのポリゴンが出力されます。<br>

- Export Animation<br>
オブジェクトの基本的な位置、回転、スケールのアニメーションが書き出されます。<br>可能な場合は、FCurve（Channel）単位でのキーフレームが書き出され、マトリクス変換が必要なキーフレームは、XYZの座標値として出力されます。<ins>ボーンのアニメーションは、サポートされていません。</ins><br>

- Bake Keyframes<br>
Bake Keyframesが有効の場合は、各フレームで評価されたXYZの座標値が書き出されます。それ以外はFCurve（Channel）単位でのキーフレームが書き出されます。


## オブジェクトデータのプル（読み込み）

YT-Bridgeのプル操作は、YT-Toolsのペーストに相当し、中間ファイルに保存されているオブジェクトデータを指定した方法でシーンに読み込みます。

- New Objects (New Items)<br>
中間ファイルに保存されているデータを新規オブジェクトとして読み込みます。<br>

- Replace Objects (Replace Items)<br>
中間ファイルに保存されているオブジェクトデータを同一名称のシーン上のオブジェクトに上書きします。シーン上に一致する名称を持つオブジェクトがない場合は、新規オブジェクトに読み込みます。

- Duplicate and Replace Objects (Duplicate and Replace Items)<br>
Replace Objectsと同一ですが、オブジェクトデータの上書きを行う前に、その元オブジェクトの複製を作成します。複製したオブジェクトは非表示に設定されます。オブジェクトデータの上書きで作業を進めたいが、念の為元データのバックアップを残しておきたい場合にこのモードを使用します。<br>

- オブジェクトタイプの選択<br>
読み込みを行うオブジェクトのタイプをトグルボタンで指定します。Mesh、Curve、Light、Camera、Empty、Armatureが指定できます。

- Replace Materials<br>
Replace Materialsを有効にすると中間ファイルに保存されているマテリアルデータで、シーン上のマテリアルデータを上書きします。読み込み先のマテリアルを優先させるには、このオプションをオフにしておく必要があります。

- Replace Object Transforms<br>
Replace Object Transformsを有効にすると中間ファイルに保存されているオブジェクトの座標値で、シーン上のオブジェクト座標値データを上書きします。読み込み先のオブジェクト座標値データを優先させるには、このオプションをオフにしておく必要があります。

- Replace Modifiers<br>
YT-Bridgeでは、Blenderのメッシュオブジェクトなどに設定されているモディファイア情報も中間ファイルに保存しています。Replace Modifiersを有効にすると中間ファイルに保存されているモディファイアのデータでシーン上のモディファイアを上書きます。モディファイアの上書きは、Blender間でのプッシュ・プル操作でのみ使用することができます。

- Setup Armature Modifiers (Setup Skeleton Deformers)<br>
このオプションを有効にすると、ボーンとVertex Groups（頂点ウェイトマップ）をマッピングするモディファイア（デフォーマー）を中間データ読み込み時にセットします。

- Import Animation<br>
オブジェクトのTransformアニメーションデータが読み込まれます。

## 名前付きファイルへの保存・読み込み（Export/Import）

YT-Bridgeでは、中間ファイルを一時ファイルとしてOSが提供するフォルダに作成し、アプリケーション間でデータの交換を行っています。Export/Importではこのデータファイルをユーザーが指定したファイル名称で任意のフォルダに保存したり、読み込む機能を提供しています。

## データ変換詳細

### オブジェクト座標データ

BlenderのオブジェクトとModoのアイテム座標データは、位置座標値、回転座標値、スケール値、回転順序がそれぞれのローカル座標系で出力されれます。Blenderの座標系は右手座標系のZ-Up、Modoの座標系は右手座標系のY-Upです。座標値は中間データファイルから読み込む際に変換されます。また、オブジェクトのペアレンティングの情報も中間ファイルに保存されます。

### リンクオブジェクト（インスタンスアイテム）

Modoのインスタンスアイテムは、Blenderのリンクオブジェクトに相互に変換されます。Blenderのリンクオブジェクトは、シーン上で最初のリンクオブジェクトが実オブジェクトとして中間ファイルに保存され、それ以降のリンクオブジェクトがインスタンスとして出力されます。
<div align="left">
<img src="images/modo_instance.png"/>
</div>
<div align="left">
<img src="images/blender_linked.png"/>
</div>
<i>Mesh Paintで作成したModoのインスタンスアイテムをBlenderのLink Objectに変換</i><br>

### Meshデータ

Meshデータは、BlenderのMeshオブジェクトのMeshデータとModoのMeshアイテムのサーフェイスタイプ（Face,SubD,PSub）のポリゴンデータを交換します。それ以外ポリゴンタイプ（TextやPolyline）は、Meshデータとして交換されません。カーブデータはCurveオブジェクトとして交換されます。<br>
頂点座標値の座標系（Blenderの座標系は右手座標系のZ-Up、Modoの座標系は右手座標系のY-Up）は、中間ファイルからの読み込み時に変換されます。<br>
ModoのStaticMeshは、Meshデータに変更して出力します。<br>

基本的な頂点、ポリゴン情報の他、下記の情報がMeshデータとして交換されます。<br>

- Polygons (Surface Type Polygons)<br>
Modoのポリゴンのうち、Face、Subdivision Surace, Catmull-Clark SubdivisionタイプのポリゴンがPolygonとして出力されます。キーホールタイプのポリゴンは、三角形に分割して出力されます。<br>
- UV Sets (UV Map)<br>
Mesh内の全てのUVマップが中間ファイルに出力されます。<br>
- Edge Crease (Subdivision Weight)<br>
Subdivision Surace, Catmull-Clark Subdivisionのエッジウェイトが中間ファイルに出力されます。<br>BlenderのSubdivisionモディファイアとの互換のため、Modoのエッジウェイト値の平方根が出力されます。<br>
- Shape Keys (Morph)<br>
Modoのモーフマップが中間ファイルに出力されます。<br>相対モーフマップおよび絶対モーフマップが出力されます。<br>
- Vertex Groups (Weight Map)<br>
Modoの頂点ウェイトマップが中間ファイルに出力され、BlenderのVertex Groupsとして読み込まれます。<br>
- Color Attributes (RGBA Map)<br>
RGBおよびRGBAマップのデータが中間ファイルに出力されます。BlenderのFloatタイプのFaceCornerのカラーアトリビュートとして読み込まれます。<br>
- Freestyle Edges, Freestyle Faces (Selection Sets)<br>
BlenderのFreestyleエッジおよび面の情報は、Modoの選択セットとして出力されます。<br>"_Freesytle"という名称のエッジ選択セットは、Freestyleのデータとして取り扱われます。<br>
- Selection Sets (Selection Sets)<br>
Modoの選択セットは、YT-Toolsが取り扱う、選択セットとして出力されます。このデータは"sset@"を接頭子に持つカスタムアトリビュートとして出力されます。<br>
- Custom Normals (Vertex Normal Map)<br>
Modoの頂点マップが中間ファイルに出力され、BlenderのCustom Normalsとして読み込まれます。<br>
- Edge Sharpness (Hard Edge Map)<br>
ModoのHard Edgeマップが中間ファイルに出力され、BlenderのEdgeシャープとして読み込まれます。<br>
- Subdivision Surface<br>
ModoのMeshのポリゴンがすべてCatmull-Clark Subdivisionだった場合、Catmull-Clarkの分割レベルの属性が中間ファイルに出力されます。<br>この情報が存在した場合、BlenderのMESHオブジェクトには、Subdivionモディファイアが追加されます。<br>
- Materials<br>
マテリアルの基本カラーおよびラフネスの値が中間ファイルに出力されます。テクスチャはカラー、ノーマルマップ、ラフネスの画像テクスチャが出力されます。<br>

### Curveデータ

Curveデータは、BlenderのCurveオブジェクトのCurveデータとModoのMeshアイテム内にあるCurve、Bezier Curve、B-Spline Curveが交換されます。ModoのCatmull-Romカーブは、Bezierカーブに変換されて出力されます。BlenderのNURBSは、ModoのB-Splineカーブに変換されて出力されます。ウェイト値は交換されません。<br>

### Cameraデータ

Cameraデータは、カメラの画角情報、レンズタイプ（パースペクティブ、並行）、焦点長、DOFの焦点距離が中間ファイルに出力されます。

### Lightデータ

Lightデータは、ライトの種類（点、スポット、エリア、指向性）の情報が出力されます。Modoの指向性ライト（Directional Light）は、BlenderのSunライトに変換されます。その他、ライトのカラーおよび強度が出力されます。ModoのIntensityとBlenderのenergyは単位が異なりますが、それぞれのスケールレンジの比率に基づいて係数(40.0)が乗算されます。(Blender energy range (0-200), Modo intensity range (0-5))<br> 

### Emptyデータ

Emptyデータは、Modoのロケータアイテムとして出力され、BlenderのEMPTYオブジェクトと交換されます。オブジェクト（アイテム）の座標データのみが出力されます。<br>

### Armatureデータ

Armatureデータは、Modoのスケルトンとして使用されているロケータアイテムのデータが、BlenderのArmatureオブジェクトのデータに変換されます。Modoのスケルトンを構成するJointアイテムとBlenderのArmatureオブジェクトのBoneはデータ構造が異なるため、複数の分岐がある親子関係の階層構造は完全には変換されません。Modoのスケルトンの先端に位置するアンカーアイテムは出力されず、BoneのTail座標値として出力されます。<br>
ModoのスケルトンはロケータアイテムをJointアイテムとして使用しているため、どのロケータがJointとして使用されているかを判断することが困難な場合があります。YT-Bridgeでは、下記のようなチェックでJointか汎用的なLocatorかを区別しています。
- アイテムにBONEのTag文字列がある場合。Skeleton Drawツールは、このBONEのTag文字列を書き込みます。
- IK Jointパッケージがアイテムに追加されている場合。Bindコマンドを実行するとIK JointパッケージとGeneral Influenceが追加されます。
- Linkチャンネルが、CustomもしくはLineに設定されている場合、Jointとして認識します。
<div align="left">
<img src="images/modo_skeleton.png"/>
</div>
<div align="left">
<img src="images/blender_armature.png"/>
</div>
<i>ModoのスケルトンをBlenderのボーンに変換</i><br>


### アニメーションデータ

アニメーションデータは、基本的なオブジェクト（アイテム）の位置、回転、スケールの値がFCurve（Channel）単位もしくは、XYZ座標値単位で交換されます。BlenderのQuaternioの回転データは、Modoではオイラー角度（XYZ）に変換されます。Bake Keyframesが有効の場合は、各フレームで評価されたXYZの座標値が書き出されます。<ins>オブジェクト（アイテム）のトランスフォーム以外のアニメーションデータは、サポートされていません。</ins><ins>また、スケルトンのボーンのアニメーションデータもサポートされていません。</ins>

### マテリアルデータ

マテリアルは、基本的なディフューズカラーとラフネスの値が出力されます。テクスチャはディフューズカラー、ノーマルマップおよびラフネスの画像テクスチャが出力されます。それ以外の画像テクスチャも出力されますが、対応するエフェクトが存在しない場合は、シーンに反映されません。基本的にマテリアルはマスターとなる側のアプリケーションで設定されているマテリアルを優先して使用することを前提にしています。<b>Replace Materials</b>オプションを有効にした時のみ、読み込んだマテリアルで既存のマテリアルを上書きします。<br>テクスチャのカラースペースは、sRGBとNone-Colorのみが明示的に変換されます。それ以外は各アプリケーションの初期値が設定されます。<br>



### モディファイア（デフォーマー）の設定

Setup Armature Modifiers (Setup Skeleton Deformers)を有効にすると、ボーンとVertex Groups（頂点ウェイトマップ）をマッピングするモディファイア（デフォーマー）を中間データ読み込み時にセットしてます。BlenderではArmatureモディファイアが、ModoではGeneral Influenceデフォーマーが設定されます。<br>



## 変更履歴

### v1.0 新規リリース

- YT-Bridge for Blenderの新規リリース


## License

This Blender add-on is licensed under the GNU General Public License v3.0 or later.

You are free to use, modify, and redistribute it under the terms of the GPL license.
For details, please see the included `LICENSE.txt`.


