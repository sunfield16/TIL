Androidの[[バックグラウンド処理]]を行う各種ライブラリを、  
設定に応じて内部で使い分けて非同期処理（タスク処理）を実現してくれるAPIクラス。

今までは種類が多くて分かりづらい状態だった非同期処理ライブラリだが、  
このWorkManagerはその各種ライブラリを統合している。  
これを使用することで、意識しなければならない事が減って開発者の負担が軽減できるだろう。

## 主な機能
* バックグラウンドでのタスク処理の実行
* タスクを遅延させて実行できる（指定した時間が経過した後に実行したい場合などに有効）
* 設定すれば、アプリや端末の再起動をした場合でも確実に実行できる
* AndroidのAPIバージョン14までカバーでき、下位互換性に優れる
* 端末の状態などに応じた「制約」をタスクにつけて、その制約を満たしている時だけ実行させられる
  - ネットワーク状態、電池の残量などまで設定可能

## 使い所
* アプリや端末の再起動に関わらず確実に実行したい場合
* タスクを作成した時点ですぐに実行しなくてもいいような場合

## 弱点
* 即時実行は苦手（作成してすぐ実行したいような場合には他のライブラリの方が強い）

## 使い方
やることは大きく分けて3つ。

* 実際に実行する内容になる`Worker`を作る
* `Worker`を動かすためのタスクである`WorkRequest`を作る
* 管理用クラスの`WorkManager`にタスクを渡す

### 事前準備
WorkManagerはライブラリなので、使う場合はgradleにちゃんと書かないといけない。  
アプリの`build.gradle`に依存関係を定義する必要がある。

``` groovy
dependencies {
    // 2019/01/15時点では、最新の安定バージョンは2.2.0
    def work_version = "2.2.0"
    
    // WorkManager関係のモジュールを使うために必要
    // 参考URLには他にもオプションがあるが、Javaでとりあえず使うならこれだけでOK
    implementation "androidx.work:work-runtime:$work_version"
}
```

参考:<<https://developer.android.com/jetpack/androidx/releases/work#declaring_dependencies>>

### Workerを作る
`Worker`は、実際に実行したい内容を表現する。  
基本的には、用意されている`Worker`クラスを継承して独自の`Worker`を作っていく。

``` java
import androidx.annotation.NonNull;
import androidx.work.Worker;
import androidx.work.WorkerParameters;

/// Workerを継承してクラスを作る
/// 今回はサンプルとして適当なログを出すクラス
public class SampleLogWorker extends Worker
{
  public SampleLogWorker(@NonNull Context context, @NonNull WorkerParameters params)
  {
    super(context, params);
  }
  
  // このメソッドをオーバーライドして、タスクでやらせたいことを書いていく
  @NonNull
  @Override
  public Result doWork()
  {
    Log.d("SimpleLogWorker", "sample logged");
    return Result.success();
  }
}
```

### Workerを動かすための設定を作る
`Worker`を作ったら、それを動かすためのタスクである`WorkRequest`を作成する。  
（`Worker`に渡す仕事を作るイメージ）

タスクとして3つのクラスがあり、場合によって使い分ける。  
それぞれ簡単に作れるように「`Builder`」があるので、これを使って作成していく。  
（下のサンプルでは一番簡単な`OneTimeWorkRequest`を使う）

``` java
// BuilderにはWorkerを指定する
OneTimeWorkRequest.Builder builderOneTime = new OneTimeWorkRequest.Builder(SampleLogWorker.class)

// とりあえずbuild()で一番簡単なタスクを作成
OneTimeWorkRequest workRequest = builderOneTime.build();
```

`Builder`には色々な設定をつけることができ、これによって遅延させて実行したりタグをつけたりできる。

``` java
OneTimeWorkRequest.Builder builderOneTime = new OneTimeWorkRequest.Builder(SampleLogWorker.class)

// 生成したBuilderに色々設定して、build()でタスク作成
OneTimeWorkRequest workRequest2 = builderOneTime
  .setInitialDelay(10, TimeUnit.MINUTES) // 10分後に起動する
  .addTag("TagHoge") // タグ「TagHoge」を付与（設定しておくと、後々タグ指定でWorkRequestを取得できる）
  .build();
```

### WorkManagerにタスクを渡す
`Worker`と`WorkRequest`ができたら、最後に管理用クラスである`WorkManager`に  
`WorkRequest`を渡して実行管理してもらう。

時間指定がなければ設定して間もなく実行されるだろうし、時間指定していれば一定時間後に起動する。

``` java
// contextは基本的にアプリケージョンのcontextを使用する
// ここでは「cocos2d-x」で開発している場合を想定して記載
Context context = Cocos2dxHelper.getActivity().getApplicationContext();

// 作成したWorkRequestを渡して、後はWorkManagerに任せる
WorkManager.getInstance(context).enqueue(workRequest);
```
