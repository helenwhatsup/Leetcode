
-------------------------------------------------------------------------------------------------------------
*#LC 721 Account Merge*


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
   
