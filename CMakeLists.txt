cmake_minimum_required(VERSION 3.10)
project(lua)
set(CMAKE_C_STANDARD 99)

include_directories(src)

AUX_SOURCE_DIRECTORY(src ALL_SRC)
set(LUA_LIB_SRC ${ALL_SRC})
list(REMOVE_ITEM LUA_LIB_SRC src/lua.c src/luac.c)

add_library(lua STATIC ${LUA_LIB_SRC})
target_link_libraries(lua m dl readline)

add_executable(luacli src/lua.c)
target_link_libraries(luacli lua)
set_target_properties(luacli PROPERTIES OUTPUT_NAME lua)

add_executable(luac src/luac.c)
target_link_libraries(luac lua)
