---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
permalink: /AttributeManager/index_J.html
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

# Attribute Manager for Blender

このアドオンは、メッシュオブジェクトの頂点、エッジ、面の属性やその他のオブジェクトの様々な属性をスプレッドシートのインターフェイスで編集する機能を提供するBlenderのツールです。<br>

## Blenderバージョン

- 4.0以上、もしくはその派生バージョン
- アドオンはPythonのみで記述されており、macOS, Windowで動作します。

## インストール

BlenderのPreferencesのAdd-onsメニューからAttributeManager.zipをインストールし、AttributeManagerを有効にします。
<div align="left">
<img src="images/addon.png"/>
</div>
<br>

## 使い方

基本的な機能は、サイドバーの"Attribute Manager"タブからアクセスできます。<b>AttributeManager</b>のパネルは水平方向に伸縮可能で、パネル左側のエッジをドラッグすることでパネルの幅を調整することができます。
また、テーブルに表示する行数は<b>Max Rows</b>の値で調整できます。デフォルトは6行です。<br>
<div align="left">
<img src="images/sideBar.png"/>
</div>
<br>

## インターフェイスの説明
<div align="left">
<img src="images/UI.png"/>
</div>
<br>

### <ins>(1) Correct Selected (Correct Objects)</ins><br>

<b>Correct Selected</b>を押すと、現在シーン上で選択されている頂点、エッジもしくは面をアトリビュートマネージャーに読み込みます。ここに読み込んだメッシュエレメントの属性がアトリビュートエディターの編集対象になります。シーン上で選択を変更したりメッシュを変更した場合は、このボタンを押して変更した情報を編集テーブルに読み込み直す必要があります。<b>Object</b>モードの場合は、指定されたオブジェクトのアトリビュートを読み込みます。<br>

### <ins>(2) 編集モード</ins><br>
アトリビュートマネージャーには、Vertex, Edge, Face, Objectの4つのモードがあります。Vertex, Edge, Faceモードでは、メッシュの頂点、エッジ、面の属性をメッシュのEdit Modeで編集いたします。モードを切り替えると自動的に選択されているメッシュエレメントが編集テーブルに読み込まれます。Objectモードでは、各オブジェクトの様々な属性を編集したします。

### <ins>(3) 編集項目</ins><br>
このエリアには編集テーブルに表示したい属性をトグルボタンで指定します。編集した項目は編集テーブルのカラムに表示されます。これにより編集に必要な項目だけを選択して編集テーブルに表示させることができます。

### <ins>(4) 編集テーブル</ins><br>
読み込んだ属性を編集するためのスプレッドシート形式の編集テーブルです。テーブル右側にある垂直スライダーを使用して、テーブルの要素をスクロールすることができます。最初の行には<b>編集項目</b>で選択した属性の名称が表示されます。Vertex, Edge, Faceモードでは、メッシュエレメントのインデックス番号が表示されます。Objectモードでは、オブジェクトの名称が表示されます。青色で表示されている行は、現在選択されている行です。

### <ins>(5) Apply to All Rows<ins><br>
<b>Apply to All Rows</b>は、現在選択されている行の指定した項目を他の全ての行に適用します。適用する項目は<b>Apply to All Rows</b>の左側にあるプルダウンメニューから選択します。

### <ins>(6) Show Indices, Show Weights<ins><br>
<b>Show Indices</b>を押すと、現在選択されいるメッシュエレメントのインデックスの数字が3D View上に表示されます。これはBlenderのEdit Mode OverlayのパネルにあるIndicesトグルボタンと同じ機能です。編集テーブル上のインデックスが3Dビュー上のどのエレメントに対応するかを確認したいときに使用します。<b>Show Weights</b>は、Vertex Groupsの頂点ウェイト値を3Dビュー上にグラデーション表示するために使用します。これはBlenderのEdit Mode OverlayのパネルにあるVertex Group Weightsトグルボタンと同じ機能です。

### <ins>(7) Max Rows<ins><br>
<b>Max Rows</b>は、編集テーブルに表示する行数を指定します。デフォルトは6行です。


## 頂点編集モード
<div align="left">
<img src="images/vertexMode.png"/>
</div>
<br>

頂点編集モードは、メッシュ頂点の座標値やシェイプキー、Vertex Groupのウェイト値などを編集するモードです。頂点およびシェイプキーの座標値はローカルとグローバルの２つの座標系で編集することができます。グローバル座標系の場合は、メッシュ頂点の座標値をグローバル座標系に変換して編集テーブルに表示し、編集した値はローカル座標系に変換してメッシュに書き戻しています。YT-Tools for Blenderの作業平面の機能と組み合わせて、作業平面上の頂点の座標値を揃えたい場合などで便利に使うことができます。シェイプキーとVertex Groupは、プルダウンメニューで選択されている対象データの値が編集対象になります。


## エッジ編集モード
<div align="left">
<img src="images/edgeMode.png"/>
</div>

エッジ編集モードは、メッシュを構成するエッジのスムース、クリースなどの属性を編集するモードです。Lengthはエッジの端点の頂点の座標値を変更し、指定した長さにエッジの中心位置を基準に長さを調整します。

## 面編集モード
<div align="left">
<img src="images/faceMode.png"/>
</div>

面編集モードは、メッシュの各面に割り付けられているマテリアルを編集するモードです。Freestyleの属性も変更可能です。

## オブジェクト編集モード
<div align="left">
<img src="images/objectMode.png"/>
</div>

オブジェクト編集モードは、オブジェクトの表示属性、オブジェクト座標データ、各オブジェクトタイプ固有の属性を編集するモードです。オブジェクトモードには、編集テーブルに読み込むオブジェクトのタイプを選択するプルダウンメニューと属性のカテゴリーを選択するプルダウンメニューがあります。オブジェクトモードでは、編集する属性が多いため、属性のカテゴリーを選択して編集作業を行います。オブジェクトのタイプを選択するプルダウンメニューでは、オブジェクトのタイプ、全てのオブジェクト、選択されているオブジェクトを選んで編集テーブルに属性を読み込むことができます。属性のカテゴリーを選択するプルダウンメニューでは、VisibilityやTransformなどのオブジェクトのタイプに共通のカテゴリーに加え、ライトやカメラなどに固有の属性のカテゴリーを選択することができます。<br>
また、オブジェクトモードでは、オブジェクトの名称を変更することができます。<b>Apply to All Rows</b>を使って他のオブジェクトに同じ名称を設定した場合、Blenderが自動的に同じ名称のオブジェクトに対して連番を付加します。例えば、一連のArmatureに対して"Bone_LeftLeg"などの名称を一括して付けたい場合などに便利です。



## 変更履歴

### v1.0 新規リリース

- Attribute Manager for Blenderの新規リリース

## License

This Blender add-on is licensed under the GNU General Public License v3.0 or later.

You are free to use, modify, and redistribute it under the terms of the GPL license.
For details, please see the included `LICENSE.txt`.
