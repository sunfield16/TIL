## 他アプリからのActivity起動を制限する
`android:exported`という項目で、  
ActivityやServiceを他のアプリから起動できるかどうかを設定することができる。

```xml
<activity  
    android:name="com.hogehoge.AppActivity"  
    android:configChanges="orientation|keyboardHidden|screenSize|screenLayout"  
    android:launchMode="singleTask"
    android:screenOrientation="portrait"
    android:exported="true">
```

trueにしている場合、他のアプリからこのActivityを起動することが可能になる。  

falseの場合でも、同じアプリ内や同じユーザーIDのアプリ（同じ会社のアプリとか）  
からであれば起動は可能。

## Android12以降
Android12以降では、インテントフィルタを使用しているActivityやServiceは  
必ず`android:exported`を明示的に指定する必要がある。

<https://developer.android.com/about/versions/12/behavior-changes-12#exported>
