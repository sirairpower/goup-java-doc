# Goup Java Collection Doc
# Interfaces
### The Collection Interface
### The Set Interface

<p>
Set 集合物件不能放置重複物件。模擬數學上的抽象集合。</br>
Set 加強了 equals(),hashCode()條件。（但是 source 上沒有很明顯展示這點?）</br>
參考：
<a href="https://stackoverflow.com/questions/12940663/does-adding-a-duplicate-value-to-a-hashset-hashmap-replace-the-previous-value">
重複的值處理方式
</a>
</p>
<p>
HashSet, TreeSet, 和 LinkedHashSet 實作 Set 介面。</br>
- HashSet 把元素放進 hash table ,效能很棒但不保證取出順序。</br>
- TreeSet 把元素放在 RB Tree,排序會按照他們的值，但會稍慢於 HashSet。</br>
- LinkedHashSet 實作於 hash table 並透過 linked list 遍歷其中，排列順需基本上就是插入時的順序，排序成本要稍高於 HashSet。
</p>

<p>
簡易去除重複的方式：

```
// java 8 之前
Collection<Type> noDups = new HashSet<Type>(c);

// java 8 之後聚合操作。
c.stream()
.collect(Collectors.toSet()); // no duplicates
```
</p>

### The List Interface
<p>
List是有序的Collection

<b><h2>Iterator</h2></br>
List類專用的 ListIterator。</br>
一般的Iterator只能remove元素，ListIterator可以add()、set()、remove()
<br>
ListIteratoru也可以在游標向後或向前previous()

<b><h2>Range-View Operation</h2></br>

<p>
    
    //subList(int fromIndex, int toIndex)

    //for (int i = fromIndex; i < toIndex; i++) {
    ...
    }
<p>
fromIndex - 截取元素的起始位置，包含该索引位置元素</br>
toIndex - 截取元素的结束位置，不包含该索引位置元素</br>

swap— 交換 a 中指定位置的元素List。</br>
copy— 將源複製List到目標List。</br>
sort—List使用合併排序算法對 a 進行排序，</br>
</P>
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

<P>Deque是一個雙端隊列 Quene和Deque 實現了 stack和Quene<br/>
Queue佇列有點像先進先出<br/>
Dequey可以對尾端加入物件或取出物件<br/>
</P>
### Wrapper Implementations
### Convenience Implementations