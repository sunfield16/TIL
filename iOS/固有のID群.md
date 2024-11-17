## UUID(Universally Unique IDentifier)
`RFC 4122`で定義されているID規格。  
生成するたびに違う値が出力され、理論上は重複しない。

Linux系のOSであれば、`uuidgen`コマンドで生成できる。

## UDID(Unique Device IDentifier)
iOS端末に存在している個体識別番号。  
iOS5以降では非推奨となり、2013/05/01以降では  
これを取得するアプリはリジェクトされる。

## UIID(Unique Installation IDentifier)
UDIDの代わりとして有志が作成した、「各端末内の各アプリごとに異なる」  
という特徴を持ったUUID。

例えば、端末内にアプリA, B, Cがあったとして  
A, B, Cそれぞれに固有のUUIDが生成される。  
このUUIDはアプリを再インストールしても変わらない。  

生成用のライブラリがMITライセンスで公開されている。  
<https://github.com/akisute/UIApplication-UIID>

### 取得できるIDのイメージ
※どちらの場合でも、アプリを再インストールでIDは変わらない。

UDID

|        | 端末1 | 端末2 | 端末3 |
| ------ | --- | --- | --- |
| アプリA | aaa | bbb | ccc |
| アプリB | aaa | bbb | ccc |
| アプリC | aaa | bbb | ccc |

UIID

|        | 端末1 | 端末2 | 端末3 |
| ------ | --- | --- | --- |
| アプリA | aaa | bbb | ccc |
| アプリB | ddd | eee | fff |
| アプリC | ggg | hhh | iii |

## 参考資料
<https://tanamon.hatenablog.jp/entry/20120924/1348491831>

<https://sites.google.com/site/aoi68k/home/ge-tiid-uuid-udidno-qu-de>

<https://akisute.com/2011/08/udiduiid.html>