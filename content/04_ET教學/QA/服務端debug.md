**使用 ComponentFactory.Create 創建出來的 Entity 數據會殘留**

這是因為 Create 預設使用了Pool物件池，所以必須在 Entity.Dispose 時清除數據才不會造成殘留


```
BomberScenarioRoom bomberScenarioRoom = 
    await BomberScenarioRoomFactory.Create(m2SStartGame);

//ComponentFactory.cs
public static T Create<T>(bool fromPool = true) where T : Component{
    Type type = typeof (T);			
    T component;
    if (fromPool)

//BomberScenarioRoom.cs
public override void Dispose(){
    //清除數據
    this.Reset();
}
public void Reset(){
    this.MathRoomId = 0;
    this.RoomId = 0;
}
```