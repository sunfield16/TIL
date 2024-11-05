## 型の変換
NSString -> std::string
```objective-c++
NSString* hoge = @"hoge";
std::string hogeCPP = [hoge UTF8String];

// Objective-C++ ならこれでもいける
std::string hogeCPP2 = hoge.UTF8String;
```
NSInt -> int
```objective-c++
NSInt index = 0;
int indexCPP = static_cast<int>(i);
```

## クロージャーを使う場合の注意
クロージャーで変数をキャプチャするとき、  
実体で渡さないと問題が起きるケースがある。
https://qiita.com/1234224576/items/7d26b98d5731a8e7af93
```objective-c++
void HogeObjCPP::func(const std::string& hogeId)
{
	// onComplete() 内でhogeIdを使えるように一時変数を用意する
	std::string temp = hogeId;
	[HogeObj fugaFunc:
			onComplete:^(BOOL success, NSError * _Nullable error)
	{
		// ↓ここで hogeId をそのまま出力すると空文字になる
		NSLog(@"success %s", temp.c_str());
	}];
}
```