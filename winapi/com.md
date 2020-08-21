# COM

## QueryInterfaceの実装方法

* `ppvObject`が`nullptr`の場合、`E_POINTER`を返す。
* `IsEqualIID`を使ってIIDを比較してキャストできる型なら、`ppvObject`に自分のポインタを渡して`AddRef`して`S_OK`を返す。
* IIDがキャストできない型なら、`E_NOINTERFACE`を返す。
