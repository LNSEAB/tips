# IMM

## コンポジションウィンドウを非表示にした時の候補ウィンドウの位置の修正方法

　候補ウィンドウは`CFS_CANDIDATEPOS`で位置を合わせようとしたとき下にズレる。
これはコンポジションウィンドウの大きさ分が候補ウィンドウの除外領域（`CANDIDATEFORM`の`CFS_EXCLUDE`、その領域に入らないように自動で修正される）に入っているので、
この領域をなくすように`CFS_EXCLUDE`の`RECT`を設定すれば候補ウィンドウの左上と`CFS_CANDIDATEPOS`の座標が合うようになる。
これを実現するには以下のコードのように`RECT`の`left`と`right`、`top`と`bottom`がそれぞれ等しくして`CFS_EXCLUDE`に設定すればよい。

```c++
POINT pt = {/* 適当な値が入ってるとする */};
RECT rc = {
    pt.x, // left
    pt.y, // top
    pt.x, // right
    pt.y, // bottom
};
```

## ImmAssociateContextEx

* 例外投げた等でメインループに入る前に終了した後、ImmAssociateContextExを呼び出すとダメっぽい（他のところでSEGVした）。
