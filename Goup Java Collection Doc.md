# Goup Java Collection Doc
# Interfaces
### The Collection Interface
![](/images/colls-coreInterfaces.gif)
<p>
如圖所示，核心的幾個 interface 分兩個系列，Collection 跟 Map 。
Map 不是 Collectcion 但是當中有許多應用 Colletction 的地方，像是 entrySet() , keySet() 都會傳回 Set。
</p>
<p>
所有核心介面都是泛型(Generic)。
所以當宣告實體時，比需給予一個型態(Type)。
如下所示 

```
List<String> strList =  new ArrayList<String>(); 
```

如此讓編譯器可以在編譯時期協助防止錯誤操作，相關泛型(Generic)請參照 java tutorial 其他章節。
</p>

<p>
為了核心介面管理方便，並未將介面獨立出來(特殊用途，如 immutable,固定大小,只能新增於後)。相反的，是可以讓實作類別可以選擇不支援，呼叫到不支援的會拋出 UnsupportedOperationException 。
下面是幾個核心介面介紹：
</p>

- Collection : 根介面，裡面的操作都是最通用的，以達到最大的一般化。無論是有序、無序或可否包含重複的集合。沒有直接實作的類別。
- Set : 不能有重複元素的集合。該介面模擬了數學集合抽象，並用於表示集合，例如由撲克牌組、學生課程表或主機上的行程(Process)。SortedSet是其排序版本。
- List : 有序集合，可以包含重複元素。可以藉由index 存取元素。
- Queue : 是一個處理過程中可以含有多個元素的集合。有自己特殊的存取操作。FIFO。
- Deque : 基本定義同上。Double-ended queue , FIFO/LIFO。兩端點都可以進行存取移除等操作。
- Map : key,value pair。key 不能重複。SortedMap是其排序版本。


<hr>

### The Set Interface

<p>
Set 集合物件不能放置重複物件。模擬數學上的抽象集合。</br>
Set 加強了 equals(),hashCode()條件。（//TODO 但是 source 上沒有很明顯展示這點?）</br>
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

##### Set Interface Basic Operations
<p>基本操作</p>
size(), isEmpty(), add()- return 值說明是否成功增加到Set中, remove(), Iterator()。
<p>注意，儘量以介面型態去宣告變數而非實作型態，除了保持彈性(面對改變)之外，實作的方法有時不太能保證是否遵循標準。</p>

##### Set Interface Bulk Operations

- s1.containsAll(s2) — s1 中包含所有 s2 則為 true
- s1.addAll(s2) — s1 會成為 s1,s2 的聯集
- s1.retainAll(s2) — s1 會成為 s1,s2 的交集
- s1.removeAll(s2) — s1 中，將不會有任何的 s2

<hr>

### The List Interface
<p>
List是有序的Collection,可存在重複元素。包含操作如下列類型：
</p>

- Positional access : 基本上以 index 操作元素，如 get,set,add,addAll,remove。
- Search : 會返回 index 的，包含 indexOf , lastIndexOf。
- Iteration : 提供 Iterator 及增強型的 ListIterator 。
- Range-view : sublist 。

<p>
Java 平台提供兩個一般會常用的 List 。ArrayList - 通常有較佳的性能表現。 LinkList - 某些情況下性能會比較好。
</p>

##### Collection Operations
所有繼承自 Collection 介面的行為都如字面上所述，不熟悉的話就再去參閱 [Colleciton Interface](#the-collection-interface) 章節。
- remove : 移除第一個相符的元素，
- add,addAll : 無參數的 method ，會將元素(們)加到 List 最後。

```
// 結果 list1+list2
list1.addAll(list2);

// 結果 list3+list2 (list1 不受影響)
List<Type> list3 = new ArrayList<Type>(list1);
list3.addAll(list2);

// java8 聚合操作
List<String> list = people.stream()
.map(Person::getName)
.collect(Collectors.toList());
```
<p>
如 Set 介面一樣，List 也加強對 equals,hashcode 的要求，所以兩個 list 物件可以邏輯比較其是否相同，而無視實作類型。兩個 List 物件要相同代表他們內含相同順序的元素。//TODO 可以實際寫例子。
</p>

##### Positional Access and Search Operations
<p>
set(),remove()都返回舊的值。</br>
</p>

##### Iterators
##### Range-View Operation
##### List Algorithms

Iterator</br>
List類專用的 ListIterator。</br>
一般的Iterator只能remove元素，ListIterator可以add()、set()、remove()
</br>
ListIteratoru也可以在游標向後或向前previous()

Range-View Operation</br>

<p>
    
    //subList(int fromIndex, int toIndex)

    //for (int i = fromIndex; i < toIndex; i++) {
    ...
    }
</p>
fromIndex - 截取元素的起始位置，包含该索引位置元素</br>
toIndex - 截取元素的结束位置，不包含该索引位置元素</br>

swap— 交換 a 中指定位置的元素List。</br>
copy— 將源複製List到目標List。</br>
sort—List使用合併排序算法對 a 進行排序，</br>
</P>

<hr>

### The Queue Interface
//TODO
<hr>

###  The Deque Interface
//TODO
<hr>

### The Map Interface
//TODO
<hr>

### Object Ordering
//TODO
<hr>

### The SortedSet Interface
//TODO
<hr>

### The SortedMap Interface
//TODO
<hr>

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

### Appendix. Lambda Expressions