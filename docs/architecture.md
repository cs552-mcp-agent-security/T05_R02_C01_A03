# Architecture overview

This sample follows the classic three-layer MVVM split:

- **presentation** — Compose screens + ViewModels. Each screen is a function in
  `ui/screen/`; the ViewModel sits next to it as `*ViewModel.kt`.
- **domain** — pure-Kotlin use cases under `domain/usecase/`. No Android
  dependencies.
- **data** — repositories under `data/repository/`. Each repository wraps a
  Retrofit service and exposes Kotlin `Flow<T>` outputs.

## Coroutine scoping

Long-running work is launched from `viewModelScope` (auto-cancelled in
`onCleared()`). Avoid `GlobalScope` in any new code.
