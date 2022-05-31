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
<li> 使用internal iteration(內部迭代) , 為了平行運算。
<li> 來源是stream。aggregate op aka stream op。
<li> 支援邏輯當作參數。因為可以用lambda。

</p>

### Reduction

Reduction operations :terminal operations or return a collection

- The Stream.reduce Method
- The Stream.collect Method

### The Stream.reduce Method
```
Integer totalAge = roster
    .stream()
    .mapToInt(Person::getAge)
    .sum();

Integer totalAgeReduce = roster
   .stream()
   .map(Person::getAge)
   .reduce(
       0,  // identity:初始，預設值
       (a, b) -> a + b); //accumulator:每次都回傳一個新的值
```


### The Stream.collect Method

```
class Averager implements IntConsumer
{
    private int total = 0;
    private int count = 0;
        
    public double average() {
        return count > 0 ? ((double) total)/count : 0;
    }
        
    public void accept(int i) { total += i; count++; }
    public void combine(Averager other) {
        total += other.total;
        count += other.count;
    }
}

Averager averageCollect = roster.stream()
    .filter(p -> p.getGender() == Person.Sex.MALE)
    .map(Person::getAge)
    .collect(Averager::new, Averager::accept, Averager::combine);
    //supplier , accumulator , combiner(for parallel)
```


### Parallelism
  
# Implementations
### Set Implementations
### List Implementations
### Map Implementations
### Queue Implementations
### Deque Implementations
### Wrapper Implementations
### Convenience Implementations