# AniLipSync-VRM
VRMモデルでリミテッドアニメ風のリップシンクを実現するためのライブラリです。
[AniLipSync](https://github.com/XVI/AniLipSync)がベースになっています。

# ダウンロード
[AniLipSync-VRM v1.0.1](https://github.com/sh-akira/AniLipSync-VRM/releases/download/v1.0.1/AniLipSync-VRM_1.0.1.unitypackage)

# 開発環境
- Windows 10
- Unity 2017.4.15f1

# 必要なライブラリ
- [OVRLipSync 1.28.0](https://developer.oculus.com/downloads/package/oculus-lipsync-unity/1.28.0/)
- [UniVRM 0.45](https://github.com/dwango/UniVRM/releases)

# サンプル
`Assets/AniLipSync-VRM/Examples/Scenes/AniLipSync-VRM.unity` にサンプルシーンがあります。  
[OVRLipSync 1.28.0](https://developer.oculus.com/downloads/package/oculus-lipsync-unity/1.28.0/)と[UniVRM 0.45](https://github.com/dwango/UniVRM/releases)をインポートし、  
[ニコニ立体ちゃんVRMモデル](https://3d.nicovideo.jp/works/td32797)をダウンロードし、AliciaSolid.vrmを
Assets/Models/AliciaSolid.vrmにフォルダを作ってコピーしてください。  
サンプルシーンを開きHierarchy上にAliciaSolidのPrefabを配置したら、AniLipSync-VRMのAnim Morph Target (Script)の  
Blend Shape ProxyにAliciaSolidを設定してください。  
実行してマイクに喋ると口が動きます。  

# 使い方
1. [OVRLipSync 1.28.0](https://developer.oculus.com/downloads/package/oculus-lipsync-unity/1.28.0/)をインポート
2. [UniVRM 0.45](https://github.com/dwango/UniVRM/releases)をインポート
3. [AniLipSync-VRM.unitypackage](https://github.com/sh-akira/AniLipSync-VRM/releases) をインポート
4. 好きなVRMモデルをインポート
5. `Assets/Oculus/LipSync/Prefabs/LipSyncInterface` プレハブをシーンに配置
6. `Assets/AniLipSync-VRM/Prefabs/AniLipSync-VRM` プレハブをシーンに配置
7. 好きなVRMモデルのプレハブをシーンに配置
5. `AniLipSync-VRM` GameObjectの `AnimMorphTarget` の各プロパティをインスペクタで編集（BlendShapeProxyにはシーンに配置したVRMモデルを入れてください）

# AnimMorphTargetの各プロパティの説明
以下説明は元の[AniLipSync](https://github.com/XVI/AniLipSync)とBlendShapeProxy以外同じです。
## Transition Curves
aa, E, ih, oh, ou のそれぞれの音素へ遷移する際に、BlendShapeの重みを時間をかけて変化させるためのカーブです。

例えば、黙っている状態から aa の音素を検知した場合、Element 0 のカーブに従って時々刻々とBlendShapeの重みを変化させます。aa の状態で ih の音素を検知した場合、Element 2 のカーブに従います。

徐々に重みを増やすことで、ゆるやかに口の形が変化するような表現が可能です。

## Curve Amplifier
Transition Curveの縦軸の値に倍率をかけます。

Transition Curveの縦軸を 0.0 ～ 1.0 の範囲にしておいて 100 の倍率をかけることで、カーブ編集時の煩雑な操作を省略できます。

## Weight Threashold
この値より小さな音素の重みを無視します。

小さなノイズ等で口が開いてしまう現象を回避できます。

## Frame Rate
1秒間にBlendShapeの重みを更新する頻度の設定です。

リミテッドアニメ風の効果を得ることができます。

## Blend Shape Proxy
BlendShapeProxyを持ったVRMモデルを指定してください。

## Smooth Amount
OVRLipSyncのSmooth amountの値を設定できます。

# 制限事項
- 声を入力してから口が動くまでに遅延があります。配信ソフトや動画編集ソフトを使用して音声を250msほど遅延させるとタイミングが合うでしょう。
- `LowLatencyLipSyncContext`はOVRLipSyncより後に実行する必要があります。AniLipSync.unitypackageのインポートで自動的に設定されますが、スクリプトのみをコピーする際は`Script Execution Order`による設定が必要です。

# ライセンス
本リポジトリに上がっている部分はMIT Licenseです。LICENSEファイルを参照してください。クレジットを記載することで、営利・非営利を問わず利用いただけます。

OVRLipSyncのライセンスについては、Oculus社のサイトを参照してください。

このライブラリは、[AniLipSync](https://github.com/XVI/AniLipSync/blob/master/LICENSE)をもとに作られています。
