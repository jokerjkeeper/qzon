**Q: ILRuntime 模式下登入返回出錯**

_BsonSerializationException: Maximum serialization depth exceeded (does the object being serialized have a circular reference?)._

A: 解答在第二章圖，因為那邊調用了 MongoHelper.toJson 在 Editor 看不到全部的 Callstack，需要去 Editor.log 查看全部的調用紀錄。

![[Pasted image 20260221013712.png]]

![[Pasted image 20260221013717.png]]

![[Pasted image 20260221013721.png]]

**Q:客戶端 export client design 出現錯誤**

A: 刪除掉 {Project}\Excel\md5.txt 重新導出

![[Pasted image 20260221013726.png]]

**Q: 在 EditWindow 使用 Sprite 發現不存在**

A: 需要引用 UnityEditor.U2D.Sprites 如下

`using UnityEditor.U2D.Sprites;`

![[Pasted image 20260221013733.png]]

[ref] [_https://docs.unity3d.com/2021.2/Documentation/Manual/UpgradeGuide2019LTS.html_](https://docs.unity3d.com/2021.2/Documentation/Manual/UpgradeGuide2019LTS.html)

_**Q:打包版本出現錯誤**_
```
Library\PackageCache\com.unity.ugui@1.0.0\Runtime\UI\Core\Image.cs(887,87): error CS1061: 'Sprite' does not contain a definition for 'isUsingPlaceholder' and no accessible extension method 'isUsingPlaceholder' accepting a first argument of type 'Sprite' could be found (are you missing a using directive or an assembly reference?)

Library\PackageCache\com.unity.ugui@1.0.0\Runtime\UI\Core\Image.cs(1865,38): error CS1061: 'SpriteAtlas' does not contain a definition for 'IsPlaceholder' and no accessible extension method 'IsPlaceholder' accepting a first argument of type 'SpriteAtlas' could be found (are you missing a using directive or an assembly reference?)
```

A:PlayerSetting 選擇 IL2CPP 會出現這個問題

![[Pasted image 20260221013739.png]]

**Q.PC包下載資源出現問題**

unity Non-secure network connections disabled in Player Settings

A: 需要將 Player Setting, Allow downloads over HTTP 改成 always allow

![[Pasted image 20260221013744.png]]

**Q.使用Arial.ttf在Unity2022版本出錯**

argumentexception: arial.ttf is no longer a valid built in font. please use legacyruntime.ttf

A.需要改用legacyruntime.ttf

![[Pasted image 20260221013749.png]]

**Q.打包apk出現問題**

**Cause: unable to find valid certification path to requested target**

![[Pasted image 20260221013753.png]]

有提到是關於網絡不穩定造成的

![[Pasted image 20260221013757.png]]

後來是在 build.gradle 添加了這行才解決的

`checkReleaseBuilds false`

![[Pasted image 20260221013802.png]]

[![Logo](https://gitbook.urscos.com/~gitbook/image?url=https%3A%2F%2Fassets.cnblogs.com%2Ffavicon_v3_2.ico&width=20&dpr=3&quality=100&sign=8ad53202&sv=2)打包Apk之Could not download groovy-all.jar (org.codehaus.groovy:groovy-all:2.4.15)以及appIcon报错 - 沫戏回首 - 博客园www.cnblogs.com](https://www.cnblogs.com/moxihuishou/p/13532240.html)

**Q.安裝到Pixel6的轟炸超人並沒有出現在桌面也搜不到**

一定要保證安裝到最後有出現Success

![[Pasted image 20260221013807.png]]

查了安裝的日誌發現不少關於網絡的Error, 開了 proxy 後終於安裝成功且出現 Success(之前都會卡在最後面不動)
![[Pasted image 20260221013811.png]]