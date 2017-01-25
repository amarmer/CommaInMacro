### Comma in macro puzzle

If a macro parameter has comma, code won't compile.

How to implement macro RESOLVE_COMMA_IN_TYPE(type), which "returns" type.
If 'type' has comma, then 'type' should be eclosed in parenthesis, but if 'type' doesn't have comma then parenthesis are not needed.

For instance map<int, int> has comma, then:
```C++
RESOLVE_COMMA_IN_TYPE((map<int, int>), m);

// It is the same as:
map<int, int> m;
```

For instance for vector<int>:
```C++
RESOLVE_COMMA_IN_TYPE(vector<int>, v); 

// It is the same as:
vector<int> v;
```

One proposed solution bellow from http://stackoverflow.com/questions/13842468/comma-in-c-c-macro but it won't compile in VS 2015.

```C++
template<typename T> struct argument_type;
template<typename T, typename U> struct argument_type<T(U)> { typedef U type; };
#define FOO(t,name) argument_type<void(t)>::type name
FOO((std::map<int, int>), map_var);
```


