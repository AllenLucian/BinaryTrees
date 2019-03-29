# BinaryTrees
- 一些二叉树相关的操作(Some operations for binary tree)



## BinaryTreePrinter
- 树状打印一棵二叉树（Print a binary tree like a real tree）
- 输入一棵二叉搜索树（input a binary search tree）: 
  -  [7, 4, 9, 2, 5, 8, 11, 1, 3, 6, 10, 12]
- 输出（output）:
```shell
         7
       /   \
     4       9
    / \     / \
   2   5   8   11
  / \   \     /  \
 1   3   6   10  12
```

- 示例（example）
  - 先实现**NodeOperation**的相关操作(Implements NodeOperation)
    - 根节点是谁？（Who is the root node?）
    - 如何查找左节点？（How to get the left child?）
    - 如何查找右节点？（How to get the right child?）
  ```java
  public class BinarySearchTree implements NodeOperation {
    /********** NodeOperation **********/
    @Override
    public Object root() {
      // tell me who is the root node
      return mRoot;
    }
  
    @Override
    public Object left(Object node) {
      // tell me how to get the left child of the node
      return ((Node)node).mLeft;
    }
  
    @Override
    public Object right(Object node) {
      // tell me how to get the right child of the node
      return ((Node)node).mRight;
    }
    /********** NodeOperation **********/
  }
  
  static BinarySearchTree<Integer> bst(Integer ints[]) {
    if (ints == null) return null;
    BinarySearchTree<Integer> bst = new BinarySearchTree<Integer>();
    for (Integer integer : ints) {
    	bst.add(integer);
    }
    return bst;
  }
  ```

  - 初始化**BinaryTreePrinter**
  ```java
  // initialize a printer
  BinaryTreePrinter printer = new BinaryTreePrinter();
  // optional setting
  // printer.setCompacted(false);
  // printer.setClosestSpace(3);
  ```
  - 打印(print)
  ```java
  BinarySearchTree<Integer> bst1 = bst(new Integer[]{
      7, 4, 9, 2, 5, 8, 11, 1, 3, 6, 10, 12
    });
  printer.println(bst1);
  /*
          7
        /   \
      4       9
     / \     / \
    2   5   8   11
   / \   \     /  \
  1   3   6   10  12
  */
  
  BinarySearchTree<Integer> bst2 = bst(new Integer[]{
      381, 12, 410, 9, 40, 394, 540, 
      35, 190, 476, 760, 146, 445,
      600, 800
    });
  printer.println(bst2);
  /*
          381
        /     \
    12           410
   /  \         /   \
  9    40     394   540
      /  \         /   \
   35    190    476     760
        /       /      /   \
      146     445    600   800
  */
  
  printer.println(bst(new Integer[]{
          30, 10, 60, 5, 20, 40, 80,
          15, 50, 70, 90
        }));
  /*
          30
       /      \
    10          60
   /  \       /    \
  5    20   40      80
      /       \    /  \
    15        50  70  90
  */
  ```

  - 也可以生成字符串写入文件(write to file)
  ```java
  // also can write to file
  String filePath = "/Users/mj/Desktop/bst.txt";
  // String filePath = "C:/test/bst.txt";
  
  // generate print string
  String printString = printer.printString(bst1);
  Files.writeToFile(filePath, printString);
  ```

- 甚至你还都不用定义二叉树类(even you don't need to create a binary tree class)
```java
printer.println(new NodeOperation() {
  @Override
  public Object root() {
  	return 8;
  }

  @Override
  public Object left(Object node) {
    if (node.equals(8)) return 3;
    if (node.equals(3)) return 1;
    if (node.equals(6)) return 4;
    if (node.equals(14)) return 13;
    return null;
  }

  @Override
  public Object right(Object node) {
    if (node.equals(8)) return 10;
    if (node.equals(10)) return 14;
    if (node.equals(3)) return 6;
    if (node.equals(6)) return 7;
    return null;
  }
});
/*
      8
    /   \
  3       10
 / \        \
1   6       14
   / \      /
  4   7   13
*/
```