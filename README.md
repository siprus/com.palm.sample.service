# ex

@ -83,7 +83,7 @@ class Struct
inline Struct( const Reference<T> &);
inline Struct<T,HANDLER> &operator=( const T &inRHS ) { value = inRHS; return *this; }
- inline Struct<T,HANDLER> &operator=( const null & ) { value = T(); }
+ inline Struct<T,HANDLER> &operator=( const null & ) { value = T(); return *this; }
inline Struct<T,HANDLER> &operator=( const Dynamic &inRHS ) { return *this = Struct<T,HANDLER>(inRHS); }
operator Dynamic() const { return CreateDynamicStruct(&value,sizeof(T),HANDLER::handler); }
operator String() const { return HANDLER::toString(value); }
bool operator==(const Struct<T,HANDLER> &inRHS) const { return value==inRHS.value; }
// Haxe uses -> notation
inline T *operator->() { return &value; }
T &get() { return value; }
static inline bool is( const Dynamic &inRHS)
{
hx::Object *ptr = inRHS.mPtr;
if (!ptr)
return false;
if (!ptr->__GetHandle())
return false;
if (ptr->__length() != sizeof(T))
return false;
return ptr->__CStr() == HANDLER::getName();
}
