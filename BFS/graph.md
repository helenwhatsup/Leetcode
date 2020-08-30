## Graph Traversal模版
--
* intialize graph

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
 --
    
        Queue<Integer> queue=new LinkedList<>();
        // Set<Integer> visitedset= new HashSet<>();
        queue.offer(0);
        //  visitedset.add(0);
        int visited=0;
        while(!queue.isEmpty()){
            int curnode=queue.poll();
            //拿出一个点，把它neighbors丢进去。
            visited++;
            for(Integer neighbor: graph.get(curnode)){
                //search in a set of nodes(neighbor)
                if(visitedset.contains(neighbor)){
                    continue;
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
    
