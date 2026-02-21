1、在資源目錄中新增對應的 ReferenceCollector Prefab, 將要使用到的資源拉到 Reference Collector 清單中，並設置 AssetBundle 為 "common/abmadventurepanel.unity3d"

![[Pasted image 20260221013645.png]]

2、打包資源後可在程式中調用取得

![[Pasted image 20260221013650.png]]

使用說明

1、將資源掛在ReferenceCollector底下，新增MapSource.prefab並將所有Map_001~Map~N掛在底下，將這個 bundle 命名為 mapsource.unity3d，並打包。

![[Pasted image 20260221013700.png]]

2、最終我們可以在程式裡面如此調用，如下:

![[Pasted image 20260221013704.png]]