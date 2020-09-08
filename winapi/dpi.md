# DPI

## マニフェストを使わないPer-Monitor Aware

* `SetProcessDpiAwarenessContext`を呼び出す。`SetProcessDpiAwareness`はWindows8.1から対応の古い関数なのでもう必要ないかもしれない。
呼び出すタイミングはアプリケーション開始時が無難（ウィンドウクラスを登録する前かウィンドウを作る前でも大丈夫なのかまで調べていない）。
コードは以下のようにしている。
```c++
inline void enable_dpi_awareness() noexcept {
    if (SetProcessDpiAwarenessContext(DPI_AWARENESS_CONTEXT_PER_MONITOR_AWARE_V2)) {
        return;
    }
    if (SetProcessDpiAwarenessContext(DPI_AWARENESS_CONTEXT_PER_MONITOR_AWARE)) {
        return;
    }
    if (SetProcessDpiAwareness(PROCESS_PER_MONITOR_DPI_AWARE) == S_OK) {
        return;
    }
}
```

* `WM_NCCREATE`で`EnableNonClientDpiScaling`を呼び出す。