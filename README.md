# arrcmp
high performance alternative to glibc's memcmp. Also demonstrating concept of using TMP with intrinsics for optimised assembly code. 

This approach was presented as a lightning talk at C++ On Sea 2022, titled: "C++ your friendly meta assembler - or how to beat memcmp" 
https://www.youtube.com/watch?v=v6ENImXcsPE

## Installing dependencies (for ubuntu)

```bash
# Google test and Google Benchmark
sudo apt install libgtest-dev libbenchmark-dev

# Google Benchmark plot
git submodule update --init --recursive 
```
## Building 
Best results with clang-14 or newer:

```bash
cmake -B build -S . -DCMAKE_BUILD_TYPE=RELEASE -DCMAKE_CXX_COMPILER=clang++-14 -DCMAKE_C_COMPILER=clang-14

cmake --build build
```

Tests and benchmarks will be run automatically


run `bench/run_and_graph_results.sh` to produce CSV results and plot them with `google_benchmark_plot/plot.py`. 

For the impatient the results, are included as CSV and png in bench folder and below...

# Sandybridge CPU (SSE2)
![image](https://user-images.githubusercontent.com/1681962/180046310-21dd9ec6-e8cb-4a66-bae7-b926470b4f0b.png)

# Skylake CPU (AVX2)
![image](https://user-images.githubusercontent.com/1681962/180046453-17c66e11-1cc6-4c67-993a-6a3510b402a9.png)

