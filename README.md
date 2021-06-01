https://github.com/BarkingBad/tasty-bug

```
sbt:scala3-simple> run
[info] running Main$package 
Class Name:
src/main/resources/tasties/B_rename.tasty
AST:
class dotty.tools.dotc.ast.Trees$PackageDef

Class Name:
src/main/resources/tasties/A.tasty
AST:
class dotty.tools.dotc.ast.Trees$PackageDef

How many Array.tasty files are there:
8
How many Array.tasty files with different size are there: 
1
Class Name:
src/main/resources/tasties/Array.tasty
AST:
class dotty.tools.dotc.ast.Trees$EmptyTree

Class Name:
src/main/resources/tasties/scala/Array.tasty
AST:
class dotty.tools.dotc.ast.Trees$PackageDef  // <--------------------- The only correct read of Array.tasty file

Class Name:
src/main/resources/tasties/scala/Array11.tasty
AST:
class dotty.tools.dotc.ast.Trees$EmptyTree

Class Name:
src/main/resources/tasties/dir/Array.tasty
AST:
class dotty.tools.dotc.ast.Trees$EmptyTree

Class Name:
src/main/resources/tasties/dir/scala/Array.tasty
AST:
class dotty.tools.dotc.ast.Trees$EmptyTree

Class Name:
src/main/resources/tasties/dir/scala/Array11.tasty
AST:
class dotty.tools.dotc.ast.Trees$EmptyTree

Class Name:
src/main/resources/tasties/dir/Array11.tasty
AST:
class dotty.tools.dotc.ast.Trees$EmptyTree

Class Name:
src/main/resources/tasties/Array11.tasty
AST:
class dotty.tools.dotc.ast.Trees$EmptyTree
```

TastyInspector correctly loads `A` and `B` tasty files, though they are at `resources/tasties/` path

TastyInspector incorrectly loads many combinations of `Array.tasty` stdlib tasty file *unless* it is exactly at `scala/Array.tasty` path suffix with *companion* `.class` file. Otherwise, it returns `EmptyTree`

It's worth noting that `A` and `B` files load correctly even with 
- different names than original
- different paths suffix
- no `.class` file at the same directory
