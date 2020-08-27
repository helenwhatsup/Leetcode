# BFS && Topological Sorting
## Q133(Clone Graph) Course Schedule
## 模版
* BFS使用队列，把每个还没有搜索到的点依次放入队列，然后再弹出队列的头部元素当做当前遍历点。


                                void bfs(TreeNode root) {
                                      List<List<Integer>> list = new ArrayList<>();
                                                Queue<TreeNode> queue = new ArrayDeque<>();
                                                queue.add(root);
                                                while (!queue.isEmpty()) {
                                                    TreeNode node = queue.poll(); // Java 的 pop 写作 poll()
                                                    if (node.left != null) {
                                                        queue.add(node.left);
                                                    }
                                                    if (node.right != null) {
                                                        queue.add(node.right);
                                                    }
                                                }
                                            }

BFS总共有两个模板：

* 如果不需要确定当前遍历到了哪一层，BFS模板如下。

        while queue 不空：
            cur = queue.pop()
            for 节点 in cur的所有相邻节点：
                if 该节点有效且未访问过：
                    queue.push(该节点)
* 如果要确定当前遍历到了哪一层，BFS模板如下。
这里增加了level表示当前遍历到二叉树中的哪一层了，也可以理解为在一个图中，现在已经走了多少步了。size表示在当前遍历层有多少个元素，也就是队列中的元素数，我们把这些元素一次性遍历完，即把当前层的所有元素都向外走了一步。

      level = 0
      while queue 不空：
          size = queue.size()
          while (size --) {
              cur = queue.pop()
              for 节点 in cur的所有相邻节点：
                  if 该节点有效且未被访问过：
                      queue.push(该节点)
          }
          level ++;
          
上面两个是通用模板，在任何题目中都可以用，是要记住的！

使用队列保存每层的所有节点，每次把队列里的原先所有节点进行出队列操作，再把每个元素的非空左右子节点进入队列。因此即可得到每层的遍历。



## 应用场景1. 层序遍历/图遍历/拓扑排序
什么是层序遍历呢？简单来说，层序遍历就是把二叉树分层，然后每一层从左到右遍历。


## 应用场景2. 最短路径

在一棵树中，一个结点到另一个结点的路径是唯一的，但在图中，结点之间可能有多条路径，其中哪条路最近呢？这一类问题称为最短路径问题。最短路径问题也是 BFS 的典型应用，而且其方法与层序遍历关系密切。

在二叉树中，BFS 可以实现一层一层的遍历。在图中同样如此。从源点出发，BFS 首先遍历到第一层结点，到源点的距离为 1，然后遍历到第二层结点，到源点的距离为 2…… 可以看到，用 BFS 的话，距离源点更近的点会先被遍历到，这样就能找到到某个点的最短路径了。


