# ---------------------------------------------------------------------------------------------------
cmake_minimum_required(VERSION 3.5.1)

# ソースファイル
# set(SRCS ...) # ex. set(SRCS rw_lock.cpp)
# file(GLOB_RECURSE SRCS "*.cpp") # リカーシブにソースを収集
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

# 実行バイナリを作る
# set(MY_BINARY "mybin")
# add_executable($MY_BINARY} ${SRCS})

# サブディレクトリを追加
# add_subdirectory(dir)

# ---------------------------------------------------------------------------------------------------
# 実行ファイル出力先
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# ライブラリ出力先
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

# コンパイルオプション
if((CMAKE_CXX_COMPILER_ID MATCHES "Intel") OR (CMAKE_CXX_COMPILER_ID MATCHES "GNU") OR (CMAKE_CXX_COMPILER_ID MATCHES "Clang"))
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -msse4.1 -rdynamic")
	set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -O0 -ggdb -D_DEBUG")
	set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -g")
	set(CMAKE_CXX_FLAGS_RELWITHDEBINFO "${CMAKE_CXX_FLAGS_RELWITHDEBINFO} -g3 -pg -D_ENABLE_GPROF")
	
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -msse4.1 -rdynamic")
	set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -O0 -ggdb -D_DEBUG")
	set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -g")
	set(CMAKE_C_FLAGS_RELWITHDEBINFO "${CMAKE_C_FLAGS_RELWITHDEBINFO} -g3 -pg -D_ENABLE_GPROF")
endif()

# コンパイルオプション表示
message("CMAKE_CXX_COMPILER_ID          : ${CMAKE_CXX_COMPILER_ID}")
message("CMAKE_CXX_FLAGS                : ${CMAKE_CXX_FLAGS}")
message("CMAKE_CXX_FLAGS_DEBUG          : ${CMAKE_CXX_FLAGS_DEBUG}")
message("CMAKE_CXX_FLAGS_RELEASE        : ${CMAKE_CXX_FLAGS_RELEASE}")
message("CMAKE_CXX_FLAGS_RELWITHDEBINFO : ${CMAKE_CXX_FLAGS_RELWITHDEBINFO}")

message("CMAKE_C_COMPILER_ID            : ${CMAKE_C_COMPILER_ID}")
message("CMAKE_C_FLAGS                  : ${CMAKE_C_FLAGS}")
message("CMAKE_C_FLAGS_DEBUG            : ${CMAKE_C_FLAGS_DEBUG}")
message("CMAKE_C_FLAGS_RELEASE          : ${CMAKE_C_FLAGS_RELEASE}")
message("CMAKE_C_FLAGS_RELWITHDEBINFO   : ${CMAKE_C_FLAGS_RELWITHDEBINFO}")

message("GLIBC_VERSION                  : ${GLIBC_VERSION}")

# コマンドのエクスポート
set(CMAKE_EXPORT_COMPILE_COMMANDS ON) # compile_command.json出力

# ---------------------------------------------------------------------------------------------------
set(PROJ_NAME rw_lock_sample) # プロジェクトに合わせて変更

# バイナリ名
set(MY_BINARY rw_lock) # プロジェクトに合わせて変更

# ソースコード
set(SRCS rwlock_cpp11.cpp)  # プロジェクトに合わせて変更

# リンクするライブラリ
set(LINK_LIBS pthread)  # プロジェクトに合わせて変更

# ---------------------------------------------------------------------------------------------------
# 必要なパッケージの追加
# find_package(BISON REQUIRED)
# find_package(FLEX REQUIRED)
# find_package(OpenSSL REQUIRED)
# ---------------------------------------------------------------------------------------------------

# ターゲットにソースを追加
add_executable(${MY_BINARY} ${SRCS})

# ターゲットにライブラリを追加
target_link_libraries(${MY_BINARY} ${LINK_LIBS})


