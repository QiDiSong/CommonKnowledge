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

