### How to resolve comma in type parameter in macro 

If a macro parameter has comma, code won't compile.

Macro RESOLVE_COMMA_IN_TYPE(type) "returns" type.
If 'type' has comma, then 'type' should be eclosed in parenthesis, but if 'type' doesn't have comma then parenthesis are not needed.

```C++
// For instance map<int, int> has comma, and code bellow is the same as: map<int, int> m;
RESOLVE_COMMA_IN_TYPE((map<int, int>)) m;
```

```C++
// For instance vector<int> doesn't have comma, parenthesis are not needed, code is the same as: vector<int> v;
RESOLVE_COMMA_IN_TYPE(vector<int>) v; 
```

One proposed solution bellow from http://stackoverflow.com/questions/13842468/comma-in-c-c-macro won't compile in VS 2015.

```C++
template<typename T> struct argument_type;
template<typename T, typename U> struct argument_type<T(U)> { typedef U type; };
#define RESOLVE_COMMA_IN_TYPE(type) argument_type<void(t)>::type

// Won't compile in VS 2015
RESOLVE_COMMA_IN_TYPE((map<int, int>)) m;
```


Macro RESOLVE_COMMA_IN_TYPE can be usefull in real C++ in another macro which parameter is a type, for instance:
```C++
JSON_PROPERTY((map<string, JsonContries>), contries_, "contries");
```

#### Implementation
```C++
struct ResolveCommaInType
{
    template <typename T> explicit operator T();
};

#define RESOLVE_COMMA_IN_TYPE(type) decltype(type (ResolveCommaInType()))
```


