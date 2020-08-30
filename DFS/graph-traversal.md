 ** 深度优先搜索
        public void dfs(){
            vertexList[0].wasVisited=true;
            displayVertex(0);
            theStack.push(0);
            while(!theStack.isEmpty()){
                int v=getAdjUnvisitedVertex(theStack.peek());
                if(v==-1)
                    theStack.pop();
                else{
                    vertexList[v].wasVisited=true;
                    displayVertex(v);
                    theStack.push(v);
                }
            }
            for(int j=0;j<nVerts;j++)
                vertexList[j].wasVisited=false;
        }
