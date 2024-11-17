<https://www.chartjs.org/docs/latest/general/data-structures.html>  
<https://qiita.com/fsd-ssk/items/f2c0faad04f690bcaed7>

Chart.jsに渡すデータはいくつかの形式が使える。

## シンプル配列
```javascript
const config = {
  type: 'bar', // 棒グラフ
  data: {
	labels: ['a', 'b'],
    datasets: [{
      data: [20, 10],
    }]
  }
}
```
`datasets`内の`data`を配列で渡す。
この場合、`labels`で指定した配列のインデックスに合わせて値が使われる。

## オブジェクト
```javascript
const cfg = {
  type: 'line', // 折れ線グラフ
  data: {
    datasets: [{
      data: [{x: 10, y: 20}, {x: 15, y: null}, {x: 20, y: 10}]
    }]
  }
}
```

```javascript
const cfg = {
  type: 'line', // 折れ線グラフ
  data: {
    datasets: [{
      data: [{x: '2016-12-25', y: 20}, {x: '2016-12-26', y: 10}]
    }]
  }
}
```
`data`を連想配列にして、ラベルをデータごとに指定する。

* x ... ラベル
	- 数値でも文字列でもOK。日付や項目など、目的に応じて決める
* y ... 実際のデータ数値

この場合、`labels`は設定しなくてもいい。  
ただし並び順を正確にしたい（日付など）場合は基本的には設定しておいた方が良い。


## カスタムプロパティ
### 横軸・縦軸があるもの
```javascript
const cfg = {
  type: 'bar', // 棒グラフ
  data: {
    datasets: [{
      data: [{id: 'A', content: {value: 300}}, {id: 'B', content: {value: 500}}]
    }]
  },
  options: {
    parsing: {
      xAxisKey: 'id',
      yAxisKey: 'content.value'
    }
  }
}
```
`parsing`のオプションを使うことで、データ内のキーを別途指定できる。  
X軸（項目）・Y軸（数値）のそれぞれに対して使いたいキーを指定する。




### 円グラフなど
```javascript
const cfg = {
  type: 'pie', // 円グラフ
  labels: ["A", "B", "C", "D", "E"],
  data: {
    datasets: [
	{
	  label: 'My Dataset',
	  data: [
	  {"id":"A", "value":10},
	  {"id":"B", "value":30},
	  {"id":"C", "value":60},
      {"id":"D", "value":25},
	  {"id":"E", "value":50}],
	}],
	options: {
	  parsing: {
	    key: 'value'
	  }
	}
  }
}
```
円グラフ・ドーナツグラフなどでもオブジェクトで指定できるが、  
その場合は`parsing`のオプションを使って  
「どのキーが値を表すのか」を指定する必要がある。  

なお、円グラフ・ドーナツグラフでは`labels`の設定が必須。  
（`parsing`でラベル用のキーを指定することはできない）