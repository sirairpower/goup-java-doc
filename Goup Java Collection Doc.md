# Goup Java Collection Doc
# Interfaces
### The Collection Interface
### The Set Interface
### The List Interface
### The Queue Interface
### The Deque Interface
### The Map Interface
### Object Ordering
### The SortedSet Interface
### The SortedMap Interface

# Aggregate Operations
<p> 
聚合操作(aggregate operations)的預備知識：lambda expressions , method references
下面一個簡短的例子說明聚合操作(aggregate operations)跟for-each語法上的差異：
</p>

    // for-each
    for (Person p : roster) {
        System.out.println(p.getName());
    }
    // aggregate op
    roster
    .stream()
    .forEach(e -> System.out.println(e.getName());
<p>
Pipelines and Streams<br/>
* pipeline 指的是一連串的聚合操作，通常會有下面元件：</p>
 
 - 一個來源:collection,array or I/O channel(java.nio.file)
 - 0-* 中間操作(intermediate op):像是filter 會產生新的stream,stream並非像collection一樣是個資料結構，而是元素序列。
 - 一個終結操作(terminal op):像是foreach產生非stream的結果(基本型態數值、集合)


<p>
Differences Between Aggregate Operations and Iterators<br/>

</p>

### Reduction
### Parallelism
  
# Implementations
### Set Implementations
### List Implementations
### Map Implementations
### Queue Implementations
### Deque Implementations
### Wrapper Implementations
### Convenience Implementations