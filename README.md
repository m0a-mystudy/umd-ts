# umd-ts


moment.jsは現在(2018/2/27)型定義ファイルがUMD未対応のようです。
UMDとは何かということでしたら[こちら](https://qiita.com/chuck0523/items/1868a4c04ab4d8cdfb23#umd)を参照下さい。

つまりは index.htmlのsrcに以下のように設定した場合に

```
	<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.20.1/moment.js"></script>
	<script src="./index.ts"></script>
```

``moment.js`` がグローバル変数``mement``に設定されます。
その場合型定義ファイルがUMDに対応していれば、以下のようにtsファイルから使うことでできます。

```index.ts
/// <reference path="../node_modules/moment/moment.d.ts"/>
alert(moment().format("YYYYMMDD hh:mm:ss"));

```
ですが対応していない場合があります。

そういう場合の暫定対応方法があります。 以下のように型定義ファイルをつくります。

```mement.custom.d.ts

import * as _moment from "moment";
export as namespace moment;
export = _moment;

```


index.tsは以下となります。

``moment.custom.d.ts`` を読みに行っています。

```index.ts
/// <reference path="./mytypes/moment.custom.d.ts"/>
alert(moment().format("YYYYMMDD hh:mm:ss"));

```

これで動きます。動く環境をこちらにおいています。
https://github.com/m0a-mystudy/umd-ts

``parcel src/index.html`` で実行して下さい

参考: https://github.com/moment/moment/pull/3688
