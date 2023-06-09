# cmake_recursive
This is an example of CMake configuration that is used to solve the well-known task of generating all possible valid combinations of parentheses.
It is solved by recursively creating subdirectories and copying the same CMakeLists.txt to them. Obviously, the directive `add_subdirectory` does the remaining job.

As an example, in the directory "(" run:
```
cmake .
```
The list of all combinations is printed, and the tree of subdirectories is created. The leave nodes of the tree are the answer to the task. To see them you can execute (in case of Linux environment):
```
tree -d -I CMakeFiles
```
or
```
tree -d -I CMakeFiles | less
```
This also shows the whole tree structure of the solution.

By default, the initial number of paired parentheses is 5, but you can change this by setting variable N directly through command line:
```
cmake . -DN=3
```

Be aware that N>8 may freeze the command line for a while.
