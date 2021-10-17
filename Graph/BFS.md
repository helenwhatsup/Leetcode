#BFS
模版
1. Shortest Path 
从源点出发，BFS 首先遍历到第一层结点，到源点的距离为 1，然后遍历到第二层结点，到源点的距离为 2…… 可以看到，用 BFS 的话，距离源点更近的点会先被遍历到，这样就能找到到某个点的最短路径了。




                        level = 0
                        while queue is not empty：
                           int size = queue.size()
                           for(int i=0;i<size;i++)(
                                cur = queue.pop()
                                for node in cur 's neighbors ：
                                    if node is not visited ：
                                        queue.push(node)
                            }
                           distance/level ++; // 当前层都被遍历完毕，distance ++


