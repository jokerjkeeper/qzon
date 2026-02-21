修改 Packages/manifest.json, 在最後面添加下面內容

Copy

```
"scopedRegistries": [
  {
    "name": "ILRuntime",
    "url": "https://registry.npmjs.org",
    "scopes": [
      "com.ourpalm"
    ]
  }
],
```

回到 Unity 會自動彈出 ILRuntime

![[Pasted image 20260221013553.png]]

![[Pasted image 20260221013557.png]]

[![Logo](https://gitbook.urscos.com/~gitbook/image?url=https%3A%2F%2Fgithub.com%2Ffluidicon.png&width=20&dpr=3&quality=100&sign=3a3bdc96&sv=2)Releases · Ourpalm/ILRuntimeGitHub](https://github.com/Ourpalm/ILRuntime/releases)

從這邊下載 VS Debugger 插件

![[Pasted image 20260221013603.png]]

雙擊安裝

![[Pasted image 20260221013609.png]]

安裝好了後在 Visual Studio 調試裡面會出現 Attach to ILRuntime , 另外 appdomain 必須添加下面功能才行

Copy

```
this.appDomain.LoadAssembly(this.dllStream, this.pdbStream, new Mono.Cecil.Pdb.PdbReaderProvider());
//開啟debug端口
this.appDomain.DebugService.StartDebugService(56000);
```