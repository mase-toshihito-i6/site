#operator new[]
* new[meta header]
* function[meta id-type]

```cpp
// 単純な配列の記憶域の確保
void* operator new[](std::size_t size) throw(std::bad_alloc);					// C++03 まで
void* operator new[](std::size_t size);											// C++11 から

// 単純な配列の記憶域の確保（例外をスローしない）
void* operator new[](std::size_t size, const std::nothrow_t&) throw();			// C++03 まで
void* operator new[](std::size_t size, const std::nothrow_t&) noexcept;			// C++11 から

// 配置newによる配列の記憶域の確保
void* operator new[](std::size_t size, void* ptr) throw();						// C++03 まで
void* operator new[](std::size_t size, void* ptr) noexcept;						// C++11 から
```
* nothrow_t[link /reference/new/nothrow_t.md]


##効果
プログラムが動的に記憶域を確保する。


##戻り値
確保した記憶域の先頭アドレスを指すポインタ。


##備考
一般にプログラム実行中の記憶域の動的確保は処理系がOSからヒープを割り当てるのに対し、placement-new では既にプログラムに割り当て済みの任意の記憶域を新たに確保を求められた際に便宜上割り当てる手法で、上手く使った場合は new / delete を大量に繰り返す必要のある処理を高速に実現しうる。


##例
```cpp
#include <iostream>
#include <new>

int main()
{
  try {
    // 3要素のint型配列を動的に作成
    // 確保失敗時にbad_alloc例外が送出される
    int* p3 = new int[3];
    delete[] p3;

    // 3要素のint型配列を動的に作成
    // 確保失敗時にヌルポインタが返される
    int* p4 = new (std::nothrow) int[3];
    delete[] p4;

    // char配列のスタック領域に、3要素のint型配列を動的に作成
    char array_field[sizeof(int) * 3] = {};
    int* p6 = new(array_field) int[3];
  }
  catch (std::bad_alloc& e) {
    std::cout << e.what() << std::endl;
    throw;
  }
}
```

###出力
```
```