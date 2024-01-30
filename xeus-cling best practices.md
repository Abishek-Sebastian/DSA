Some rules while coding in xeus-cling:

1. In cling, don't write the whole program code. It's like a script language. Just write the lines that should be evaluated. 
2. Don't write the main function, instead all code without a function is taken as the function.
3. Function definition is allowed in cling but then its not allowed to write other code into the same cell.
4. Do not put a ";" at the end of the last line in the cell, to see the computation result.
5. This is C++ : everything can be defined only once. Running a code twice, that defines the same variable or a function, will give a compiler error. To rerun restart the kernel/compiler.
6. All functions and variables have to be uniquely named. Follow: {Letter}_{variable/fn name} naming convention
7. Enclose the code contained in a cell using {.} in order to create a closed scope for the variables and hence enabling multiple reruns.
8. Do not define two functions in the same cell.
9. Add ";;" after lambdas. Eg. auto same = [](int i) { return i; };;
10. Higher order functions : pass input functions by universal reference.
Eg.
Wrong:
int add1(int i) { return i + 1; }
---
// This higher order function capture its input function (f) by copy
auto call_twice = [] (auto f) {
    return [&](auto x) {
      return f(f(x)); 
    };
};;
---
auto add2 = call_twice(add1);;
---

Right:
int add1(int i) { return i + 1; }
---
// This higher order function capture its input by universal reference (&&)
auto call_twice = [] (auto && f) {
    return [&](auto x) {
      return f(f(x)); 
    };
};;
---
auto add2 = call_twice(add1);;
---