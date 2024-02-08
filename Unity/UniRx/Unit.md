OnNextでイベントを通知する場合、「意味のない値」として`Unit`型が用意されている。

「シーン読み込み完了時」など、タイミングや通知そのものが重要なイベントで使う。
```csharp
private Subject<Unit> sceneSubject = new Subject<Unit>();

// メッセージを通知する時
sceneSubject.OnNext(Unit.Default)
```