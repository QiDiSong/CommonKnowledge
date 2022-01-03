C++字符串匹配

```C++
const char *reg_esp = "[ ,.\\t\\n;:]";
std::regex rgx(reg_esp) ;
std::cmatch match ;  
const char *target = "Polytechnic University of Turin " ;

if( regex_search( target, match, rgx ) ) {
  const size_t n = match.size();
  for( size_t a = 0 ; a < n ; a++ ) {
    string str( match[a].first, match[a].second ) ;
    cout << str << "\n" ;
  }
}
```

```
#include<iostream>
#include<regex>

using namespace std;

int main() {
    string data;
    cin >> data;
    long long num = 0;
    string a = "zoom.us";
    string b = "zoomgov.com";
    int c = data.find(a);
    int d = data.find(b);
   
    if (c == -1 && d == -1) {
        cout << 0 << endl;
    }
    else {
        regex pattern("\\d{9,11}");	
        smatch result;
        string::const_iterator iterStart = data.begin();
        string::const_iterator iterEnd = data.end();
        string temp;
        while (regex_search(iterStart, iterEnd, result, pattern))
        {
            temp = result[0];
            for (auto& t : temp) {
                num = num * 10 + (t-'0');
            }
            
            break;
        }
        cout << num << endl;
    }
    return 0;
}

```

