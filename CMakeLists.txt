cmake_minimum_required(VERSION 3.13...3.27)

project(sqlite3 C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

pico_sdk_init()


# SQLite3 library
add_library(libsqlite3 INTERFACE)
target_sources(libsqlite3 INTERFACE
  src/sqlite3.c
  src/fallback.c
)
target_include_directories(libsqlite3 INTERFACE src)
target_compile_options(libsqlite3 INTERFACE
  -Os
  -Wno-unused-parameter -Wno-implicit-fallthrough -Wno-char-subscripts
  -Wno-unused-but-set-variable -Wno-missing-field-initializers
  -Wno-unused-variable -Wno-unused-value
  -DPICO_SDK=1
  -DHAVE_NANOSLEEP=0
  -DSQLITE_DEFAULT_MMAP_SIZE=0
  -DSQLITE_DEFAULT_WORKER_THREADS=0
  -DSQLITE_DISABLE_DIRSYNC=1
  -DSQLITE_ENABLE_LOCKING_STYLE=0
  -DSQLITE_MAX_MEMORY=131072
  -DSQLITE_MAX_MMAP_SIZE=0
  -DSQLITE_MAX_WORKER_THREADS=0
  -DSQLITE_OMIT_AUTHORIZATION
  -DSQLITE_OMIT_BUILTIN_TEST
  -DSQLITE_OMIT_DEPRECATED
  -DSQLITE_OMIT_JSON
  -DSQLITE_OMIT_LOAD_EXTENSION
  -DSQLITE_OMIT_POPEN
  -DSQLITE_OMIT_PROGRESS_CALLBACK
  -DSQLITE_OMIT_RANDOMNESS
  -DSQLITE_OMIT_SHARED_CACHE
  -DSQLITE_OMIT_TRACE
  -DSQLITE_OMIT_UTF16
  -DSQLITE_OMIT_WAL
  -DSQLITE_TEMP_STORE=0
  -DSQLITE_THREADSAFE=0
  -DSQLITE_UNTESTABLE
)
target_link_libraries(libsqlite3 INTERFACE pico_stdlib)
