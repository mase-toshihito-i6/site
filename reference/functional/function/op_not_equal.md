#operator!=
* functional[meta header]
* std[meta namespace]
* function[meta id-type]
* cpp11[meta cpp]

```cpp
namespace std {
template <class R, class... ArgTypes>
bool operator!=(const function<R(ArgTypes...)>& f, nullptr_t) noexcept;

template <class R, class... ArgTypes>
bool operator!=(nullptr_t, const function<R(ArgTypes...)>& f) noexcept;
}
```
* nullptr_t[link /reference/cstddef/nullptr_t.md]

##概要
非等値比較する。


##戻り値
`static_cast<bool>(f)`


##例
```cpp
#include <iostream>
#include <functional>

int ident(int x) { return x; }

int main()
{
  std::function<int(int)> f = ident;

  if (f != nullptr) {
    std::cout << "not empty" << std::endl;
  }

  f = nullptr;
  if (f != nullptr) {}
  else {
    std::cout << "empty" << std::endl;
  }
}
```

###出力
```
not empty
empty
```


##バージョン
###言語
- C++11


###処理系
- [Clang, C++11 mode](/implementation.md#clang): 3.0
- [GCC, C++11 mode](/implementation.md#gcc): 4.6.4
- [Visual C++](/implementation.md#visual_cpp): ??


##参照

