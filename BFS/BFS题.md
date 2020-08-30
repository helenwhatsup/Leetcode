## Q133
          class Solution {
              public Node cloneGraph(Node node) {
                  if(node==null){
                      return null;
                  }
                   // use a queue to help BFS
                  // first add node to the queue.
                   Queue<Node> queue=new LinkedList<>();
                  queue.add(node);

                  //copy nodes
                  HashMap<Node,Node> mapping = new HashMap<>();
                  mapping.put(node,new Node(node.val));

                //bfs copy neighbors:
                  while(!queue.isEmpty()){
                      Node curnode=queue.poll();
                      //for neights of this node
                      for(Node neighbor: curnode.neighbors){
                          //如果map中没有这个点的neighbor
                          if(!mapping.containsKey(neighbor)){
                              //加入map，加入queue
                              mapping.put(neighbor,new Node(neighbor.val));
                              queue.add(neighbor);
                          }
                          //copy neighbor
                          //map.get(curnode) 就是新的Node，然后新的Node的neighbors再加入neighbor。
                          mapping.get(curnode).neighbors.add(mapping.get(neighbor));
                      }

                  }
                  return mapping.get(node);

              }

          }

## Q 261 

          class Solution {
              public boolean validTree(int n, int[][] edges) {
                //思路： 从0出发，看访问所有node的个数。每访问一个 visited++。
          //如果是树的话，所有的节点必须是连接的，也就是说必须是连通图，而且不能有环，所以焦点就变成了验证是否是连通图和是否含有环。
          //所以通过一个点0出发，看访问所有节点个数是不是n。（能不能全部访问）。 

                  //initialize graph
                  Map<Integer,Set<Integer>> graph = intialgraph(n,edges);
                  if(n==0){
                      return false;
                  }
                  //1. 基本条件
                  if(edges.length!=n-1){
                      return false;
                  }
                  // 2.判断连通性，通过一个点找所有的点
                  Queue<Integer> queue=new LinkedList<>();
                  Set<Integer> visitedset= new HashSet<>();
                  queue.offer(0);
                  visitedset.add(0);
                  int visited=0;
                  while(!queue.isEmpty()){
                      int curnode=queue.poll();
                      //拿出一个点，把它neighbors丢进去。
                      visited++;
                      for(Integer neighbor: graph.get(curnode)){
                          //search in a set of nodes(neighbor)
                          if(visitedset.contains(neighbor)){
                              continue;
              //undirected graph， 不可以直接return false 因为1联通0 0也联通1 
                          }
                          queue.offer(neighbor);
                          visitedset.add(neighbor);
                      } 
                  }
                   if(visited==n){
                          return true;
                      }
                      return false;
              }

              private Map<Integer,Set<Integer>> intialgraph (int n, int[][]edges){
                   Map<Integer,Set<Integer>> graph = new HashMap<>();
                  for(int i=0;i<n;i++ ){
                      graph.put(i,new HashSet<Integer>());
                  }
                  for(int i=0;i<edges.length;i++){
                      int u=edges[i][0];
                      int v=edges[i][1];
                      graph.get(u).add(v);
                      graph.get(v).add(u);

                  }
                  return graph;
              }
          }

