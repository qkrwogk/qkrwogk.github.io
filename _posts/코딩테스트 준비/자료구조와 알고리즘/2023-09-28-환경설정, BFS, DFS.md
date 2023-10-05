# 코딩 테스트 준비

## 230928

### 맥, VSCode 환경에서 bits/stdc++.h include하기

/Library/Developer/CommandLineTools/usr/include 등등 블로그에서 찾아본 대로 넣어도 라이브러리 path가 다른지 안먹히더라. <br /><br />

결국 학습메모 1 보고 `/usr/local/include`에다 추가해줬더니 잘 되었다. 나도 이사람처럼 homebrew로 gcc 설치했었나보다.

<img width="500" alt="스크린샷 2023-09-28 오후 7 22 03" src="https://user-images.githubusercontent.com/138586629/271251566-1cad1458-eca7-4933-86ca-931281721268.png">

근데 이것저것 해도 몇몇 헤더파일이 없는지 에러가 나서, 꼭 필요한 C++로 주석처리된 부분까지만 남기고 다 지웠다. (정확히는 C++14까지)

```h
// C++
#include <complex>
#include <deque>
#include <exception>
#include <fstream>
#include <functional>
#include <iomanip>
#include <ios>
#include <iosfwd>
#include <iostream>
#include <istream>
#include <iterator>
#include <limits>
#include <list>
#include <locale>
#include <map>
#include <memory>
#include <new>
#include <numeric>
#include <ostream>
#include <queue>
#include <set>
#include <sstream>
#include <stack>
#include <stdexcept>
#include <streambuf>
#include <string>
#include <typeinfo>
#include <utility>
#include <valarray>
#include <vector>

#if __cplusplus >= 201103L
#include <array>
#include <atomic>
#include <chrono>
#include <codecvt>
#include <condition_variable>
#include <forward_list>
#include <future>
#include <initializer_list>
#include <mutex>
#include <random>
#include <ratio>
#include <regex>
#include <scoped_allocator>
#include <system_error>
#include <thread>
#include <tuple>
#include <typeindex>
#include <type_traits>
#include <unordered_map>
#include <unordered_set>
#endif

#if __cplusplus >= 201402L
#include <shared_mutex>
#endif
```

---

잘 되나 테스트.

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> vec(10, 1);
    vector<int>::iterator iter;
    cout << "test\n" << vec[5] << "\n";

    int cnt=0;
    for (auto i: vec) {
        cnt++;
        vec[i] = cnt;
        cout << vec[i] << " ";
    }
}
```

<img width="332" alt="스크린샷 2023-09-28 오후 7 39 09" src="https://user-images.githubusercontent.com/138586629/271256013-a9fadc6b-a885-4065-bc52-7dbd240f830a.png">

bits/stdc++만 불러와도 iostream, vector 이런게 잘 불러와짐을 확인할 수 있었다.

### BFS, DFS

학습메모 3, 4를 참고해서 2차원 배열 BFS, DFS를 맛봤다.

#### BFS

```cpp
#include <bits/stdc++.h>
using namespace std;
#define X first
#define Y second

int board[502][502] = {
    {1,1,1,0,1,0,0,0,0,0}, 
    {1,0,0,0,1,0,0,0,0,0}, 
    {1,1,1,0,1,0,0,0,0,0}, 
    {1,1,0,0,1,0,0,0,0,0}, 
    {0,1,0,0,0,0,0,0,0,0}, 
    {0,0,0,0,0,0,0,0,0,0}, 
    {0,0,0,0,0,0,0,0,0,0},
 }; // 1이 파란 칸, 0이 빨간 칸에 대응
bool vis[502][502];
int n = 7, m = 10;
int dx[4] = {1, 0, -1, 0};
int dy[4] = {0, 1, 0, -1};

int main(void) {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    
    queue<pair<int, int>> Q;
    vis[0][0] = 1;
    Q.push({0, 0});

    cout << "====== [BFS] ======\n";
    for (int i=0; i<7; i++) { // 출력
        for (int j=0; j<10; j++) {
            cout << board[i][j] << " ";
        }
        cout << "\n";
    }

    while(!Q.empty()) {
        pair<int, int> cur = Q.front(); Q.pop();
        cout << "(" << cur.X << ", " << cur.Y << ") \n -> ";
        for (int dir = 0; dir < 4; dir++) {
            int nx = cur.X + dx[dir];
            int ny = cur.Y + dy[dir];
            if (nx < 0 || nx >= n || ny < 0 || ny >= m) continue;
            if (vis[nx][ny] || board[nx][ny] != 1) continue;
            vis[nx][ny] = 1;
            Q.push({nx, ny});
        }
    }
}
```

#### DFS

```cpp
#include <bits/stdc++.h>
using namespace std;
#define X first
#define Y second

int board[502][502] = {
    {1,1,1,0,1,0,0,0,0,0}, 
    {1,0,0,0,1,0,0,0,0,0}, 
    {1,1,1,0,1,0,0,0,0,0}, 
    {1,1,0,0,1,0,0,0,0,0}, 
    {0,1,0,0,0,0,0,0,0,0}, 
    {0,0,0,0,0,0,0,0,0,0}, 
    {0,0,0,0,0,0,0,0,0,0},
 }; // 1이 파란 칸, 0이 빨간 칸에 대응
bool vis[502][502];
int n = 7, m = 10;
int dx[4] = {1, 0, -1, 0};
int dy[4] = {0, 1, 0, -1};

int main(void) {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    
    stack<pair<int, int>> S;
    vis[0][0] = 1;
    S.push({0, 0});

    cout << "====== [DFS] ======\n";
    for (int i=0; i<7; i++) { // 출력
        for (int j=0; j<10; j++) {
            cout << board[i][j] << " ";
        }
        cout << "\n";
    }

    while(!S.empty()) {
        pair<int, int> cur = S.top(); S.pop();
        cout << "(" << cur.X << ", " << cur.Y << ") \n -> ";
        for (int dir = 0; dir < 4; dir++) {
            int nx = cur.X + dx[dir];
            int ny = cur.Y + dy[dir];
            if (nx < 0 || nx >= n || ny < 0 || ny >= m) continue;
            if (vis[nx][ny] || board[nx][ny] != 1) continue;
            vis[nx][ny] = 1;
            S.push({nx, ny});
        }
    }
}
```

---

<img width="315" alt="스크린샷 2023-09-28 오후 8 07 38" src="https://user-images.githubusercontent.com/138586629/271262906-35f80af5-e17e-4835-a74c-92fd989187d7.png">

<img width="327" alt="스크린샷 2023-09-28 오후 8 07 45" src="https://user-images.githubusercontent.com/138586629/271262923-228ae63d-d3cf-4e8b-a799-e075fa5d70ff.png">

잘 됨!



### 학습메모

1. [맥에서 bits/stdc++.h 사용하기](https://coder38611.tistory.com/144)
2. [stdc++.h 코드(github)](https://github.com/gcc-mirror/gcc/blob/master/libstdc%2B%2B-v3/include/precompiled/stdc%2B%2B.h)
3. [2차월 배열 BFS](https://github.com/encrypted-def/basic-algo-lecture/blob/master/0x09/BFS.cpp)
4. [2차원 배열 DFS](https://blog.encrypted.gg/942)