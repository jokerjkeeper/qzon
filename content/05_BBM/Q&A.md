1) 啟用 ILRuntime 後需要為 ETHotfix 裡面的callback函數註冊對應的 RegisterMethodDelegate

![[Pasted image 20260222013658.png]]

Copy

```
// Regist Callback Delegate, like 
appdomain.DelegateManager.RegisterMethodDelegate<System.Int32[]>();
```

![[Pasted image 20260222013702.png]]

2) 如上需要註冊對應解析函數

```
//註冊callback delegate
appdomain.DelegateManager.RegisterMethodDelegate<System.Object>();

//用於以下的地方
CoroutineMgr.RegInvokeFunc(new CoroutineMgr.RegistInvokeKey("BomberScenarioRoom_UpdateLogic", GameDefine.FrameTimeF,
    new CoroutineMgr.IK_Func(this.UpdateLogic), null));
```

![[Pasted image 20260222013746.png]]

![[Pasted image 20260222013738.png]]

3)開啟 ILRuntime 不可以使用二維數組， 用了會造成直接 crash

![[Pasted image 20260222013753.png]]

4) ILRuntime Dictionary ctor' for which no ahead of time (AOT) code was generat

需要執行 Tools/ILRuntime/Generate Binding Analysis 重新生成綁定代碼

![[Pasted image 20260222013802.png]]

5) MongoHelper序列化改用 Json，因為沒有對應的AOT生成代碼

![[Pasted image 20260222013809.png]]

6) 打包Android出現錯誤

_OBSOLETE - Providing Android resources in Assets/Plugins/Android/res is deprecated, please_

Unity2021版本之後不允許將 res 直接放在 {UnityProject}/Plugins/Android/ ，需要用 Android Studio 打包 AAR 再放到 {UnityProject}/Plugins/Android/ 目錄下

![[Pasted image 20260222013818.png]]

[https://blog.csdn.net/egostudio/article/details/123456114](https://blog.csdn.net/egostudio/article/details/123456114)

[https://blog.csdn.net/egostudio/article/details/125655477blog.csdn.net](https://blog.csdn.net/egostudio/article/details/125655477)

7) 打包APK出現問題

Could not download groovy-all-2.4.15.jar (org.codehaus.groovy:groovy-all:2.4.15)

![[Pasted image 20260222013829.png]]

修改 build.gradle 加入

```
checkReleaseBuilds false
```

```
lintOptions {
//PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderExcep
      checkReleaseBuilds false
      abortOnError false
  }
```

8) 打包出錯

2023-10-25 16:43:45.883 24254-24318/com.ujp.bbm E/Unity: NotSupportedException: G:/OlgCase/bbm/AndroidProject/export/unityLibrary/src/main/Il2CppOutputProject/IL2CPP/libil2cpp/icalls/mscorlib/System/AppDomain.cpp(168) : Unsupported internal call for IL2CPP:AppDomain::LoadAssemblyRaw - "This icall is not supported by il2cpp."

**項目打包到 Androir , Scripting Backend 必須使用 il2cpp**

![[Pasted image 20260222013847.png]]

而打包 **Hotfix.dll** 資源時沒有設定 **ILRuntime** 則打包出來的就是 Mono, 必須加 **IlRuntime** 到 Script Compilation 再打包才行

![[Pasted image 20260222013854.png]]

9) 警告信息

Parent of RectTransform is being set with parent property. Consider using the SetParent method instead, with the worldPositionStays argument set to false. This will retain local orientation and scale rather than world orientation and scale, which can prevent common UI scaling issues

**transform.parent = recycleParent; 寫法要改成 transform.SetParent(recycleParent);**

10) message 數據關聯出問題

客戶端將 Proto 宣告的 message 數據進行保存, 但保存的數據會全部刷新成最新的 message 數據造成問題

GameFrameMessage.FrameId 會變成最新的數據, 所以客戶端必須宣告新的 class 用來保存對應數據

![[Pasted image 20260222013900.png]]