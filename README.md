### Comma in macro puzzle

If a macro parameter has comma, code won't compile.

How to implement macro RESOLVE_COMMA_IN_TYPE(type), which "returns" type.
If 'type' has comma, then 'type' should be eclosed in parenthesis, but if 'type' doesn't have comma then parenthesis are not needed.

```C++
// For instance map<int, int> has comma, then:

// The same as: map<int, int> m;
RESOLVE_COMMA_IN_TYPE((map<int, int>)) m;
```

```C++
// For instance vector<int> doesn't have comma, then parenthesis are not needed:

// The same as: vector<int> v;
RESOLVE_COMMA_IN_TYPE(vector<int>) v; 
```

One proposed solution bellow from http://stackoverflow.com/questions/13842468/comma-in-c-c-macro won't compile in VS 2015.

```C++
template<typename T> struct argument_type;
template<typename T, typename U> struct argument_type<T(U)> { typedef U type; };
#define RESOLVE_COMMA_IN_TYPE(type) argument_type<void(t)>::type

// Won't compile in VS 2015
RESOLVE_COMMA_IN_TYPE((std::map<int, int>)) m;
```


