機能（Features）は、アプリがAPIから特定の種類のデータに  
アクセスできるようにする承認メカニズム。  

[アクセス許可](/Facebook/Permissions.md)とは違いユーザーから要求はできず、  
[ユーザーのロール](/Facebook/Developer/AppRole.md)や[アプリのモード](/Facebook/Developer/AppMode.md)に応じて  
有効・無効が切り替わる。

機能には以下のようなものがある。

* `Groups API` ... アプリがFacebookのグループのコンテンツにアクセスできる
  - アプリからグループに投稿したり、利用者のグループの投稿内容を取得できる
* `Page Mentioning` ... ページのメンション機能が使える
  - そのアプリが管理するページに投稿する時、他のページにメンションできる