## Gradleのバージョンを更新
Gradleのバージョンを更新するには以下を編集する。
```
[プロジェクトルート]/gradle/wrapper/gradle-wrapper.properties
```

```properties
# ここのバージョンを書き換える
distributionUrl=https\://services.gradle.org/distributions/gradle-6.5-all.zip
```

## AndroidGradleプラグインの更新
AndroidGradleプラグインを更新する場合は以下を編集する。
```
[プロジェクトルート]/build.gradle
```

```groovy
buildscript {
	repositories {
		// AndroidGradleプラグイン3.0以降を使う場合は
		// googleのリポジトリが必要
		google()
	}
	
	dependencies {
		// ここのバージョンを書き換える
		// `4.+`みたいに動的バージョンにすると予期しないアップデートがあったりするため、
		// 基本的には定数にする
		classpath 'com.android.tools.build:gradle:4.2.0'
	}
}
```

AndroidGradleプラグインを使うにはGradleも一定バージョン以上必要になるため、  
それぞれの対応に注意する。  
（対応表は公式に記載あり）  
<https://developer.android.com/studio/releases/gradle-plugin?hl=ja#updating-gradle>

## AndroidStudioから更新する
AndroidStudioからでもGradleバージョンは更新できる。
```
[File] > [Project Structure] > [Project]
```