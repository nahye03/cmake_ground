#CACHE를 사용하지 않으면 외부에서 사용할 수 없다
set(LOCAL_STRING_VARIABLE "hello world")
set(LOCAL_BOOL_VARIAbLE FALSE)

#CACHE를 사용해서 전연변수를 만듦 -> 어디서든 불러서 사용할 수 있다다
set(GLOBAL_STRING_VARIABLE "hello world" CACHE STRING "global string variable")
set(GLOBAL_BOOL_VARIABLE FALSE CACHE BOOL "global bool variable")
