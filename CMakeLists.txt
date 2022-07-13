cmake_minimum_required(VERSION 3.15)
project(hibp)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

if (MSVC)
  set(PROJECT_COMPILE_OPTIONS /W3)
  string(APPEND CMAKE_CXX_FLAGS_DEBUG " /fsanitize=address")
else() # unix'ish
  set(PROJECT_COMPILE_OPTIONS -Wall -Wextra -Wpedantic -Wshadow -Wextra-semi
    -Wmissing-noreturn -Wconversion -Wsign-conversion -Wno-ignored-attributes)
    if (NOT MINGW) # sanitizers are not working under mingw
      string(APPEND CMAKE_CXX_FLAGS_DEBUG " -fsanitize=address,undefined,leak")
    endif()
endif()

# add_subdirectory(ext/fmt)
# if (NOT MSVC)
#   target_compile_options(fmt INTERFACE -Wno-missing-noreturn)
# endif()

add_library(arrcmp INTERFACE)
target_include_directories(arrcmp INTERFACE include)
target_compile_features(arrcmp INTERFACE cxx_std_20)
# target_link_libraries(arrcmp INTERFACE fmt)


option(ARRCMP_TEST "Enable ARRCMP tests" ON)
if(ARRCMP_TEST)
  enable_testing()
  add_subdirectory(test)
else(ARRCMP_TEST)
  message(STATUS "ARRCMP Tests are disabled. Set ARRCMP_TEST to ON to run tests.")
endif(ARRCMP_TEST)

# benchmarks
option(ARRCMP_BENCH "Build ARRCMP benchmarks" ON)
if(ARRCMP_BENCH)
  add_subdirectory(bench)
else(ARRCMP_BENCH)
  message(STATUS "Building ARRCMP benchmarks is disabled. Set ARRCMP_BENCH to ON to build them.")
endif(ARRCMP_BENCH)

