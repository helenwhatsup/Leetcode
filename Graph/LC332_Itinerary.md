      *LC332 Itinerary*: sort and poll().
      
      
      class Solution {
          Map<String, PriorityQueue<String>> targets = new HashMap<>();
          List<String> route = new LinkedList();

          public List<String> findItinerary(List<List<String>> tickets) {
          //Just Eulerian path. Greedy DFS, building the route backwards when retreating.

               for (List<String>ticket : tickets){
                  targets.computeIfAbsent(ticket.get(0), k -> new PriorityQueue()).add(ticket.get(1));
               }
              visit("JFK");
              return route;

          }

          public void visit(String airport) {
              while(targets.containsKey(airport) && !targets.get(airport).isEmpty())
                  visit(targets.get(airport).poll());
              route.add(0, airport);
          }
      }
