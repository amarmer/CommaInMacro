### How to resolve comma in type parameter in macro 

If a macro parameter has comma, code won't compile.

Macro RESOLVE_COMMA_IN_TYPE(type) "returns" type.
If 'type' has comma, then 'type' should be eclosed in parenthesis, but if 'type' doesn't have comma then parenthesis are not needed.

```C++
// For instance map<int, int> has comma, and code bellow is the same as: map<int, int> m;
RESOLVE_COMMA_IN_TYPE((map<int, int>)) m;
```

```C++
// For instance vector<int> doesn't have comma, parenthesis are not needed, the same as: vector<int> v;
RESOLVE_COMMA_IN_TYPE(vector<int>) v; 
```

Macro RESOLVE_COMMA_IN_TYPE can be usefull in another macro which parameter is a type, for instance:
```C++
#define JSON_PROPERTY(type, var, name)  JsonProperty<RESOLVE_COMMA_IN_TYPE(type)> var{key(name)}; 

JSON_PROPERTY((map<string, JsonCountries>), countries_, "countries");
```


### Implementation
```C++
struct ResolveCommaInType
{
    template <typename T> explicit operator T();
};

#define RESOLVE_COMMA_IN_TYPE(type) decltype(type (ResolveCommaInType()))
```


