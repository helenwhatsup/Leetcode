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
}
----------
  #LC 721 Account Merge
   class Solution {
    public List<List<String>> accountsMerge(List<List<String>> accounts) {
        Map<String, Integer> emailToNameId = new HashMap<>();
        
         DisjointSet dsu = new DisjointSet(accounts.size());
        
        int n = accounts.size();
        for(int i=0;i<accounts.size();i++){
            for(int j=1;j<accounts.get(i).size();j++){
                String email=accounts.get(i).get(j);
                int currentNameId = i;
                if(emailToNameId.containsKey(email)){
                    int oldMapID= emailToNameId.get(email); 
                        // 同一个email两个名字。 same email with different name or entries
                    dsu.union(oldMapID,currentNameId);
                    //johnsmith@mail.com ->0 
                    // johnsmith@mail.com -> 1
                }else{
                    emailToNameId.put(email,currentNameId);
                    
                }
            }
        }
         Map<Integer, TreeSet> idToEmailMap = new HashMap<>();
            for (int i = 0; i < n; i++) {
            int rootParent = dsu.find(i); //p[0] -> 1
            List<String> email = accounts.get(i);
            idToEmailMap.putIfAbsent(rootParent, new TreeSet<>()); 
                // emails of 0 and 1 will come under parent 1
            idToEmailMap.get(rootParent).addAll(email.subList(1,email.size()));
        }
          List<List<String>> res = new LinkedList<>();
        
        for (int id: idToEmailMap.keySet()) {
            String name = accounts.get(id).get(0);
            List<String> emails = new LinkedList<>(idToEmailMap.get(id));
            emails.add(0,name);
            res.add(emails);
        }
        return res;
        
    }
}

    class DisjointSet {
        private int[] parent;
        private int[] rank;

        public DisjointSet(int n) {
            parent = new int[n];
            for(int i = 0; i<n; i++) {
                parent[i] = i;
            }
            rank = new int[n];
        }

        public int find(int x) {
            if(parent[x] == x)
                return x;
            return parent[x] = find(parent[x]);
        }

        public void union(int x, int y) {
            int rootX = find(x);
            int rootY = find(y);

            if(rootX == rootY)
                return;

            if(rank[rootX]<rank[rootY])
                parent[rootX] = rootY;
            else if(rank[rootX]>rank[rootY])
                parent[rootY] = rootX;
            else {
                parent[rootX] = rootY;
                rank[rootY]++;
            }
        }
    }
   
   
   
Segment tree
Trie 
Krusual Minum Spanning Tree
Binary indexed tree
dijkstra
floyd warshall
bellmen ford
