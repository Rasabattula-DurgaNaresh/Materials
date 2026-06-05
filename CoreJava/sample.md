                              Iterable
                                  |
                                  |
                             Collection
                                  |
        -------------------------------------------------
        |                 |                |            |
        |                 |                |            |
       List              Set             Queue        Deque
        |                 |                |            |
  ----------------   -------------    ------------   -----------
  |      |     |     |     |    |      |          |   |         |
Array  Linked Vector Hash Linked Tree Priority Array Linked
List   List          Set   HashSet Set  Queue    Deque List
                       |            |
                  (HashMap)   (Red-Black Tree)



                              Map
                               |
         ------------------------------------------------
         |                     |                       |
      HashMap           LinkedHashMap              TreeMap
         |                     |                       |
   Hash Table          Hash Table +              Red-Black
   + Buckets           Linked List                 Tree
         |
    ConcurrentHashMap
         |
     CAS + Locks