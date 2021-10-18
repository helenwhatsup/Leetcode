## DetectCycle
DFS



         private boolean isCyclic()  { 

                boolean[] visited = new boolean[V]; 
                boolean[] recStack = new boolean[V]; 

                for (int i = 0; i < V; i++) 
                    if (isCyclicUtil(i, visited, recStack)) 
                        return true; 
                return false; 
            } 
           

           private boolean isCyclicUtil(int i, boolean[] visited,  boolean[] recStack)  { 

                // Mark the current node as visited and part of recursion stack 
                if (recStack[i])  return true; 
                if not visited[i]:
                  visited[i] = true; 

                  recStack[i] = true; 
                  List<Integer> children = adj.get(i); 

                  for (Integer c: children) 
                      if (not visited[c] && isCyclicUtil(c, visited, recStack)) 
                          return true; 
                      else if recStack[c] return true; // node c is already visited ,check recursion stack 

                recStack[i] = false; 

                return false; 
            } 
  
