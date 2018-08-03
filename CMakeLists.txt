cmake_minimum_required(VERSION 3.5.1)

# ソースファイル
# set(SRCS ...) # ex. set(SRCS rw_lock.cpp)
# file(GLOB_RECURSE SRCS "*.cpp")
# add_executable(${PROJ_NAME} ${SRCS})

# include pathの追加
# set(INCUDE_DIRS ...)
# include_directories(${INCLUDE_DIRS})

# linkするライブラリの追加
# set(LINK_LIBS ...) # ex. set(LINK_LIBS pthread)
# target_link_libraries(${PROJ_NAME} ${LINK_LIBS})

# ライブラリを作る
# set(MY_LIBRALY_NAME "mylib")
# add_library(${MY_LIBRARY} STATIC srcs...)

set(PROJ_NAME rw_lock)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -msse4.1 -rdynamic")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -O0 -ggdb -D_DEBUG")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -g")

set(SRCS rw_lock.cpp)
add_executable(${PROJ_NAME} rw_lock.cpp)

set(LINK_LIBS pthread)
target_link_libraries(${PROJ_NAME} ${LINK_LIBS})
