# algorithm
前端算法

## 二叉树
`
class buildingNode {
      constructor(key, value) {
        /**
         * 创建二叉树节点
         * 节点具有：指向父节点、左子节点、右节点的指针，自身的data属性（下部代码中的key、value）
        */
        this.parent = null;
        this.left = null;
        this.right = null;
        this.key = key;
        this.value = value;
      }
    }
    /**
     * 创建二叉搜索树
     * root指向根节点指针
    */
    class buildingSearchTree {
      constructor() {
        this.root = null
      }
      static createNode(key, value) {
        return new buildingNode(key, value)
      }
      /**
       * 节点插入
       * parent记录插入位置的父节点指针
       * tail记录插入位置
      */
      insert(node) {
        let parent = this.root;
        let tail = this.root;
        // 循环判断，找到插入位置
        while (tail) {
          // 更新父节点位置
          parent = tail;
          // 判断流向
          if (node.key < tail.key) {
            tail = tail.left
          } else {
            tail = tail.right
          }
        }
        // 如果没有根节点，则直接作为根节点
        if (!parent) {
          this.root = node;
          return;
        }
        // 通过循环，找到插入位置的父节点，判断后插入
        if (node.key < parent.key) {
          parent.left = node;
        } else {
          parent.right = node;
        }
        node.parent = parent
      }
      /**
       * 搜索
       * 同插入一样，逐层搜索
      */
     search(key) {
       let parent = this.root
       if (!parent) {
         return;
       }
       while (parent && parent.key !== key) {
         if (key < parent.key) {
           parent = parent.left
         } else {
           parent = parent.right
         }
       }
       return parent
     }
     /**
      * 遍历
      * 中序遍历：先遍历左节点，再自己，最后右节点
      * 前序遍历：先遍历自己，再左节点，最后右节点
      * 后序遍历：先遍历左节点，再右节点，最后自己
     */
     traverse() {
       return this._traverse(this.root)
     }
     *_traverse(node) {
      //  通过判断处理父节点的左子节点或右子节点为空的情况
       if (node.left) {
        yield* this._traverse(node.left);
       }
       yield node;
       if (node.right) {
        yield* this._traverse(node.right);
       }
     }
    }
    let node1 = buildingSearchTree.createNode(20, '根节点')
    let node2 = buildingSearchTree.createNode(14, '二级节点')
    let node3 = buildingSearchTree.createNode(45, '二级节点')
    let node4 = buildingSearchTree.createNode(5, '三级节点')
    let node5 = buildingSearchTree.createNode(19, '三级节点')
    let node6 = buildingSearchTree.createNode(44, '三级节点')
    let node7 = buildingSearchTree.createNode(50, '三级节点')
    let tree = new buildingSearchTree()
    tree.insert(node1)
    tree.insert(node2)
    tree.insert(node3)
    tree.insert(node4)
    tree.insert(node5)
    tree.insert(node6)
    tree.insert(node7)
    let arr = [...tree.traverse()].map(item => { return item.key })
`
