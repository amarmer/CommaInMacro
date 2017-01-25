### Comma in macro puzzle

How to implement macro RESOLVE_COMMA_IN_TYPE, which allow to put backets in type which has comma 
and allow to not use backet for type which doesn't have comma.

For Instance:
RESOLVE_COMMA_IN_TYPE((map<int, int>)) m;

RESOLVE_COMMA_IN_TYPE(vector<int>) v;

Then another macro, for instance DECLARE_VAR, can be implemented like #define DECLARE_VAR(t, v) RESOLVE_COMMA_IN_TYPE(t) v;
And can be used like DECLARE_VAR((map<int, int>), m) if type has comma, and like DECLARE_VAR(vector<int>, v) if type doesn't have comma. 

