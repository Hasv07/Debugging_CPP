## Compilation
##### - run g++ compilation command 
```cpp
g++ Matrix.cpp -o Matrix
```
##### - output
```cpp
Matrix 1:
1 2 3 
4 5 6 
Matrix 2:
7 8 
9 10 
11 12 
Result of multiplication:
33 36 
66 72 
```
###### *The output of multiplication is wrong
## Debugging
After Take a look of code I suspect this Line:
```Cpp
43 result.data[i][j] = data[i][k] * other.data[k][j];

```
so lets start c++ debugger
##### - recompile with debugger flag -g
```
g++ -g Matrix.cpp -o Matrix
```
##### - run debugger command
```
gdb Matrix
```
##### - add breakpoint to the suspect Line

```
b 43
```
##### - run program
```
r
```
##### - trace result.data variable
```cpp
1- std::vector of length 2, capacity 2 = {std::vector of length 2, capacity 2 = {0, 0}, 
  std::vector of length 2, capacity 2 = {0, 0}}
2- std::vector of length 2, capacity 2 = {std::vector of length 2, capacity 2 = {7, 0}, 
  std::vector of length 2, capacity 2 = {0, 0}}
3- $4 = std::vector of length 2, capacity 2 = {std::vector of length 2, capacity 2 = {18, 0}, 
  std::vector of length 2, capacity 2 = {0, 0}}

  
```
###### *From tracing we notice results.data[0][0] change from 7 (1 x 7) to 18 (2x9) instead of adding cumulative
##### - bug fixing
```cpp 
43    result.data[i][j] += data[i][k] * other.data[k][j]; //adding + solve it
```
##### - recompile and run again
```cpp
g++  Matrix.cpp -o Matrix
./Matrix
//output
Matrix 1:
1 2 3 
4 5 6 
Matrix 2:
7 8 
9 10 
11 12 
Result of multiplication:
58 64 
139 154 
```
