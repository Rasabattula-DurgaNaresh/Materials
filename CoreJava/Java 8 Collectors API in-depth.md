# Java 8 Collectors API in-depth

**Collectors** is a 
<span style="color:green"><b>public final class</b></span> 
that extends 
<span style="color:purple"><b>Object class</b></span>.

- **Collectors class provides various useful reduction operations, such as accumulating elements into collections, summarizing elements according to various criteria, etc.**

## 📊 <span style="color:blue"><b>Java 8 Collectors Methods</span>


## <span style="color:blue"><b>🔹 Basic </span>

<table border="1" cellpadding="8" cellspacing="0">
  <thead style="background-color:#1f4e79; color:white;">
    <tr>
      <th>Method</th>
      <th>Description</th>
      <th>Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>toList()</b></td>
      <td>Collect elements into List</td>
      <td><code>stream.collect(Collectors.toList())</code></td>
    </tr>
    <tr>
      <td><b>toSet()</b></td>
      <td>Collect elements into Set</td>
      <td><code>stream.collect(Collectors.toSet())</code></td>
    </tr>
    <tr>
      <td><b>toCollection()</b></td>
      <td>Custom collection</td>
      <td><code>Collectors.toCollection(ArrayList::new)</code></td>
    </tr>
  </tbody>
</table>


## <span style="color:blue"><b>🔹 Map </span>

<table border="1" cellpadding="8" cellspacing="0">
  <thead style="background-color:#1f4e79; color:white;">
    <tr>
      <th>Method</th>
      <th>Description</th>
      <th>Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>toMap()</b></td>
      <td>Convert stream to Map</td>
      <td><code>Collectors.toMap(k,v)</code></td>
    </tr>
    <tr>
      <td><b>toMap() (merge)</b></td>
      <td>Handle duplicate keys</td>
      <td><code>Collectors.toMap(k,v,(a,b)-&gt;a+b)</code></td>
    </tr>
    <tr>
      <td><b>toConcurrentMap()</b></td>
      <td>Thread-safe map</td>
      <td><code>Collectors.toConcurrentMap(k,v)</code></td>
    </tr>
  </tbody>
</table>


## <span style="color:blue"><b>🔹 Grouping & Partitioning</span>

<table border="1" cellpadding="8" cellspacing="0">
  <thead style="background-color:#1f4e79; color:white;">
    <tr>
      <th>Method</th>
      <th>Description</th>
      <th>Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>groupingBy()</b></td>
      <td>Group elements by key</td>
      <td><code>Collectors.groupingBy(String::length)</code></td>
    </tr>
    <tr>
      <td><b>groupingByConcurrent()</b></td>
      <td>Concurrent grouping</td>
      <td><code>Collectors.groupingByConcurrent(...)</code></td>
    </tr>
    <tr>
      <td><b>partitioningBy()</b></td>
      <td>Split into two groups</td>
      <td><code>Collectors.partitioningBy(x-&gt;x%2==0)</code></td>
    </tr>
  </tbody>
</table>


## <span style="color:blue"><b>🔹 Counting & Statistics </span>

<table border="1" cellpadding="8" cellspacing="0">
  <thead style="background-color:#1f4e79; color:white;">
    <tr>
      <th>Method</th>
      <th>Description</th>
      <th>Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>counting()</b></td>
      <td>Count elements</td>
      <td><code>Collectors.counting()</code></td>
    </tr>
    <tr>
      <td><b>summingInt()</b></td>
      <td>Sum int values</td>
      <td><code>Collectors.summingInt(x-&gt;x)</code></td>
    </tr>
    <tr>
      <td><b>summingLong()</b></td>
      <td>Sum long values</td>
      <td><code>Collectors.summingLong(x-&gt;x)</code></td>
    </tr>
    <tr>
      <td><b>summingDouble()</b></td>
      <td>Sum double values</td>
      <td><code>Collectors.summingDouble(x-&gt;x)</code></td>
    </tr>
    <tr>
      <td><b>averagingInt()</b></td>
      <td>Average int values</td>
      <td><code>Collectors.averagingInt(x-&gt;x)</code></td>
    </tr>
    <tr>
      <td><b>averagingLong()</b></td>
      <td>Average long values</td>
      <td><code>Collectors.averagingLong(x-&gt;x)</code></td>
    </tr>
    <tr>
      <td><b>averagingDouble()</b></td>
      <td>Average double values</td>
      <td><code>Collectors.averagingDouble(x-&gt;x)</code></td>
    </tr>
    <tr>
      <td><b>summarizingInt()</b></td>
      <td>Int summary statistics</td>
      <td><code>Collectors.summarizingInt(x-&gt;x)</code></td>
    </tr>
    <tr>
      <td><b>summarizingLong()</b></td>
      <td>Long summary statistics</td>
      <td><code>Collectors.summarizingLong(x-&gt;x)</code></td>
    </tr>
    <tr>
      <td><b>summarizingDouble()</b></td>
      <td>Double summary statistics</td>
      <td><code>Collectors.summarizingDouble(x-&gt;x)</code></td>
    </tr>
  </tbody>
</table>


## <span style="color:blue"><b>🔹 Reduction & Transformation </span>

<table border="1" cellpadding="8" cellspacing="0">
  <thead style="background-color:#1f4e79; color:white;">
    <tr>
      <th>Method</th>
      <th>Description</th>
      <th>Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>reducing()</b></td>
      <td>General reduction</td>
      <td><code>Collectors.reducing(0, Integer::sum)</code></td>
    </tr>
    <tr>
      <td><b>mapping()</b></td>
      <td>Apply mapping before collect</td>
      <td><code>Collectors.mapping(String::length, Collectors.toList())</code></td>
    </tr>
    <tr>
      <td><b>collectingAndThen()</b></td>
      <td>Modify final result</td>
      <td><code>Collectors.collectingAndThen(toList(), Collections::unmodifiableList)</code></td>
    </tr>
  </tbody>
</table>


## <span style="color:blue"><b>🔹 String Operations </span>

<table border="1" cellpadding="8" cellspacing="0">
  <thead style="background-color:#1f4e79; color:white;">
    <tr>
      <th>Method</th>
      <th>Description</th>
      <th>Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>joining()</b></td>
      <td>Join elements</td>
      <td><code>Collectors.joining()</code></td>
    </tr>
    <tr>
      <td><b>joining(delimiter)</b></td>
      <td>Join with delimiter</td>
      <td><code>Collectors.joining(",")</code></td>
    </tr>
    <tr>
      <td><b>joining(delimiter,prefix,suffix)</b></td>
      <td>Full control join</td>
      <td><code>Collectors.joining(",", "[", "]")</code></td>
    </tr>
  </tbody>
</table>


## <span style="color:blue"><b> 🔹 Min / Max </span>

<table border="1" cellpadding="8" cellspacing="0">
  <thead style="background-color:#1f4e79; color:white;">
    <tr>
      <th>Method</th>
      <th>Description</th>
      <th>Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>maxBy()</b></td>
      <td>Find max element</td>
      <td><code>Collectors.maxBy(Comparator.naturalOrder())</code></td>
    </tr>
    <tr>
      <td><b>minBy()</b></td>
      <td>Find min element</td>
      <td><code>Collectors.minBy(Comparator.naturalOrder())</code></td>
    </tr>
  </tbody>
</table>

### 📌 Note

**All methods in the Collectors class are static.**  
👉 So, it is good to use **static import**.

### We will be using the below Employee class
```java
class Employee {
private int id;
private String name;
private int age;
private String region;
private double sal;
 
public Employee(int id, String name, int age, String region, double sal) {
this.id = id;
this.name = name;
this.age = age;
this.region = region;
this.sal = sal;
}
 
// Standard setters and getters
}
```

### Creating an Employee List.
```java
List<Employee> employeeList = new ArrayList<>();
employeeList.add(new Employee(100, "Sundar", 47, "North America", 450000));
employeeList.add(new Employee(200, "Pichai", 25, "North America", 50000));
employeeList.add(new Employee(300, "Larry", 30, "Asia", 450000));
employeeList.add(new Employee(400, "Page", 59, "Africa", 450000));
```

**<span style="color:blue"><b> Java 8 Stream.collect() Example** </span>

- Java 8’s most powerful stream method is collect() method. Which is also called a Terminal method. This is part of Stream API.

- It allows us to perform mutable fold operations (repackaging elements to some data structures and applying some additional logic,         concatenating them, etc.) on data elements held in a Stream instance.

- The strategy for this operation is provided via Collector interface implementation.

### <span style="color:blue"><b>  **Collectors.toList() Example** </span>
- toList() collector can be used for collecting all Stream elements into a List instance.

- Example to collect all employee names into List using toList() method.

```java
List<String> namesList = employeeList.stream()
                                     .map(e -> e.getName())
                                     .collect(Collectors.toList());
System.out.println(namesList);

**Output: 🔴 [Sundar, Pichai, Larry, Page]**
```

- But, there are no guarantees on the type, mutability, serializability, or thread-safety of the List returned.

- If you need more control over what type of List should be returned then should use **toCollection(Supplier)** method.

### <span style="color:blue"><b> Collectors.toSet() Example </span>
toSet() collector is used for collecting all Stream elements into a Set instance. 

Example to collect all the regions into Set.

```java
Set<String> regionSet = employeeList.stream()
                                    .map(e -> e.getRegion())
                                    .collect(Collectors.toSet());
System.out.println(regionSet);

**Output: 🔴  [Asia, Africa, North America]**
```
- But, there are no guarantees on the type, mutability, serializability, or thread-safety of the Set returned.
### 📌 Note If you need more control over what type of Set should be returned then should use the toCollection(Supplier) method.

### <span style="color:blue"><b>  Collectors.toUnmodifiableSet() Example </span>

- This collects the elements into an unmodifiable set.

- The set is created using the toSet() method can be modified. 


```java
Set<String> unmodifiableSet  = employeeList.stream()
                                    .map(e -> e.getSal())
                                    .collect(Collectors.toUnmodifiableSet());
System.out.println(unmodifiableSet);

**Output:** 🔴 [450000.0, 50000.0]
```


<b>If we try to modify set then will throw <span style="color:red">UnsupportedOperationException.</span></b>

<span style="color:blue"><b> unmodifiableSet.add(10983d); </span>

```java
Exception in thread "main" java.lang.UnsupportedOperationException
```

<b>The returned collector does not allow null values. This will throw NullPointerException if it is presented with a null value.</b>

```java
employeeList.add(null);
Set<Employee> empSet = employeeList.stream().collect(Collectors.toUnmodifiableSet());

**Output:** 🔴 The above code will cause NullPointerException. The same will be in the case of the toSet() method
```

### <span style="color:blue"><b> Collectors.toUnmodifiableList() Example </span> 
- This is similar to the toList() but toUnmodifiableList will collect elements into an unmodifiable List.

```java
Set<String> unmodifiableList   = employeeList.stream()
                                    .map(e -> e.getSal())
                                    .collect(Collectors.toUnmodifiableList());
System.out.println(unmodifiableList );

**Output:** 🔴 	[450000.0, 50000.0, 450000.0, 450000.0]
```  
- This list holds duplicates, unlike Set.

### 📌 <span style="color:red">If List has null value then it will throw java.lang.NullPointerException like toUnmodifiableSet.</span>

### <span style="color:blue"><b> Collectors.toCollection() Example </span> 
- As you probably already noticed, when using toSet() and toList() collectors, you can’t make any assumptions of their implementations. 

- If you want to use a custom implementation or LinkedList or TreeSet, you will need to use the toCollection collector with a provided collection of your choice.

- Example to collect the names into LinkedList as opposed to default List implementation.

```java
Set<String> namesLinkedList    = employeeList.stream()
                              .map(e -> e.getName())
                              .collect(Collectors.toCollection(LinkedList::new));
System.out.println(namesLinkedList  );

**Output:** 🔴 	[Sundar, Pichai, Larry, Page]
```  

### <b>Another example to collect regions into TreeSet.</b>

```java
Set<String> regionTreeSet = employeeList.stream()
                                     .map(e -> e.getRegion())
                                     .collect(Collectors.toCollection
                                     (TreeSet::new));
System.out.println(regionTreeSet);
**Output:** 🔴 	[Africa, Asia, North America]
```
### 📌 <span style="color:red">Note: This method does not work with immutable objects. In such type of cases, We must write custom Collector implementation or Use collectingAndThen().</span>

### <span style="color:blue"><b> Collectors.toMap() Example </span>
- toMap() Syntax:

```java
public static <T,K,U> Collector<T,?,Map<K,U>> toMap(Function<? super T,? extends K> keyMapper, Function<? super T,? extends U> valueMapper)
```

- Using toMap() method, A stream can be converted into a Map. But, this method needs two parameters.

- <span style="color:blue"><b>keyMapper </span>

-  <span style="color:blue"><b>valueMapper</span>

- These two are implementations of Function Functional Interface.

- Functional Interface Function has a functional method R apply(T t) that accepts one argument and produces a result.

- keyMapper will be used for extracting a Map key from a Stream element, and valueMapper will be used for extracting a value associated with a given key.

- Now, We will create a map from a stream such that the map key is emp id and value is corresponding employee object.

- keyMapper = (e) -> e.getId()
e refers to the Employee object and getting its id by calling getId() method.

- valueMapper =  Function.identity()
This method returns a function that always returns its input argument.

- Function.identity() method does take one object as an argument and returns the same object with no change.

```java
Map<Integer, Employee> empMap = employeeList.stream()
                                    .collect(Collectors.toMap((e) -> e.getId(), 
                                    Function.identity()));
System.out.println(empMap);

**Output:** 🔴 		
{400=Employee [id=400, name=Page, age=59, region=Africa, sal=450000.0], 100=Employee [id=100, name=Sundar, age=47, region=North America, sal=450000.0], 200=Employee [id=200, name=Pichai, age=25, region=North America, sal=50000.0], 300=Employee [id=300, name=Larry, age=30, region=Asia, sal=450000.0]}
```

- What happens if employeeList has duplicate employees with the same employee id.

- Now adding a duplicate emp object with the same emp id but the different name “Larry Page”.
  
```java
employeeList.add(new Employee(400, "Larry Page", 59, "Africa", 450000));

	
Map<Integer, Employee> empDupMap = employeeList.stream()
                                    .collect(Collectors.toMap((e) -> e.getId(),
                                     Function.identity()));
```

<span style="color:red"><b> Will throw the Runtime Exception as follow. </span>

```java
Exception in thread "main" java.lang.IllegalStateException: Duplicate key 400 (attempted merging values Employee [id=400, name=Page, age=59, region=Africa, sal=450000.0] and Employee [id=400, name=Page, age=59, region=Africa, sal=450000.0])
at java.base/java.util.stream.Collectors.duplicateKeyException(Collectors.java:133)
at java.base/java.util.stream.Collectors.lambda$uniqKeysMapAccumulator$1(Collectors.java:180)
```
- toMap() function takes 3rd argument as BinaryOperator Functional Interface which has a functional method R apply(T t, U u). 
- This functional method takes two arguments. In our case, the first argument takes the original employee, Second argument takes the duplicate employee and returns the employee object.

```java
Map<Integer, Employee> empDupMap = employeeList.stream()
                                       .collect(Collectors.toMap((e) -> e.getId(), 
                                       Function.identity(), 
                                       (emp, sameEmp) -> sameEmp));
System.out.println(empDupMap);
```