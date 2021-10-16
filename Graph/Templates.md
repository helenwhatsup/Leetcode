## Graph Traversal Template

*1. Build Graph*
   
         for (List<String> account : accounts) {
            String userName = account.get(0);
            for (int i = 1; i < account.size(); i++) {
                if (!graph.containsKey(account.get(i))) {
                    graph.put(account.get(i), new HashSet<>());
                }
                name.put(account.get(i), userName);
                
                if (i == 1) continue;
                graph.get(account.get(i)).add(account.get(i - 1));
                graph.get(account.get(i - 1)).add(account.get(i));
            }
        }


*2. Search* 
2.1 DFS BFS
 **DFS**
 
 
            for(String email: name.keySet()){
                         List<String> list = new ArrayList<>();
                        if (visited.add(email)) {
                            dfs(graph,email,visited,list);
                            Collections.sort(list);
                            list.add(0, name.get(email));
                            res.add(list);

                        } 
                }

   
          public void dfs(Map<String, Set<String>> graph, String email, Set<String> visited, List<String> list) {
                 list.add(email);
                 for (String next : graph.get(email)) {
                     if (visited.add(next)) {
                         dfs(graph, next, visited, list);
                     }
                 }


   
2.2 Union Find 
Union find structure allows you to group individual things together by giving all of the cells belonging to an island a label
   
  

      dsu.find(node x), which outputs a unique id so that two nodes have the same id if and only if they are in the same connected component, and:
      dsu.union(node x, node y), which draws an edge (x, y) in the graph, connecting the components with id find(x) and find(y) together.

    public void union(int[]parent,int i,int j){
        int x=find(parent,i);
        int y=find(parent,j);
        if(x!=y){
                parent[x]=y;
            }
        
    }
    public int find(int[]parent,int i){ // 返回i的根结点。
            if(parent[i]==i) return i;
            //Such nodes have their parents indicated by a -1 说明是一个cluster
            return find(parent, parent[i]); //继续找parent[i]的parent

   
   
Segment tree
Trie 
Krusual Minum Spanning Tree
Binary indexed tree
dijkstra
floyd warshall
bellmen ford
