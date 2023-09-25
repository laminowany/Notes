# Order of Evaluation
[back to index](./INDEX.md)

## Evaluation of Expressions
Evaluation of each **expression** includes:
- **value computations**
  - calculation of value that is returned by expression
- **initiation of side effects**
  - access(read/write) to an object
  - modifiation of object
  - calling I/O function
  - calling a function that does on of the above

## Ordering
**"sequenced-before"** is an asymmetric, transitive, pair-wise relationship between evaluations within the same thread.

If A is sequenced before B, then evaluation of A will be complete before evaluation of B begins.

If A is not sequenced before B and B is not sequenced before A, then two possibilities exist:
- evaluations of A and B are **unsequenced**: they may be performed in any order and may overlap (within a single thread of execution, the compiler may interleave the CPU instructions that comprise A and B)
- evaluations of A and B are **indeterminately sequenced**: they may be performed in any order but may not overlap: either A will be complete before B, or B will be complete before A. The order may be the opposite the next time the same expression is evaluated.

## Rules
For rules about how expressions are **sequenced** look [HERE](https://en.cppreference.com/w/language/eval_order#Rules)

## Undefined Behavior
- if a side effect on a scalar object is unsequenced relative to another side effect on the same scalar object
  - `i = ++i + i++;`
- if a side effect on a scalar object is unsequenced relative to a value computation using the value of the same scalar object
  - `auto n = ++i + i;`  