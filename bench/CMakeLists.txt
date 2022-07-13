

add_library(asmlib INTERFACE)
target_include_directories(asmlib INTERFACE ${CMAKE_SOURCE_DIR}/ext/asmlib)
target_link_directories(asmlib INTERFACE ${CMAKE_SOURCE_DIR}/ext/asmlib)
if (WIN32)
    target_link_libraries(asmlib INTERFACE acof64) # COF format
else()
    target_link_libraries(asmlib INTERFACE aelf64) # ELF format
endif()

find_package(benchmark REQUIRED)

add_executable(bench_arrcmp bench_arrcmp.cpp)
target_compile_options(bench_arrcmp PRIVATE ${PROJECT_COMPILE_OPTIONS})
target_link_libraries(bench_arrcmp arrcmp asmlib benchmark::benchmark)

add_executable(bench_ordering bench_ordering.cpp)
target_compile_options(bench_ordering PRIVATE ${PROJECT_COMPILE_OPTIONS})
target_compile_features(bench_ordering PRIVATE cxx_std_20)
target_link_libraries(bench_ordering arrcmp asmlib benchmark::benchmark)


