# arrcmp
high performance alternative to glibc's memcmp. Also demonstrating concept of using TMP with intrinsics for optimised assembly code. 

This approach was presented as a lightning talk at C++ On Sea 2022, titled: "C++ your friendly meta assembler - or how to beat memcmp" 

[link to talk on youtube when available]

Best results with clang-14 or newer:

```sh

cmake -B build -S . -DCMAKE_BUILD_TYPE=RELEASE -DCMAKE_CXX_COMPILER=clang++-14 -DCMAKE_C_COMPILER=clang-14

cmake --build build
```

Tests and benchmarks will be run automatically


run `bench/run_and_graph_results.sh` to produce CSV results and plot them with `google_benchmark_plot/plot.py`. 

For the impatient the results are included as CSV and png in bench folder. 
