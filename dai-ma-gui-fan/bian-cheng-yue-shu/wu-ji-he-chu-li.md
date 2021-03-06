# \(五\) 集合处理

1.\*\*【强制】\*\*关于hashCode和equals的处理，遵循如下规则：

* 只要重写equals，就必须重写hashCode。
* 因为Set存储的是不重复的对象，依据hashCode和equals进行判断，所以Set存储的对象必须重写这两个方法。
* 如果自定义对象做为Map的键，那么必须重写hashCode和equals。

```text
正例：String重写了hashCode和equals方法，所以我们可以非常愉快地使用String对象作为key来使用。
```

2.\*\*【强制】\*\*ArrayList的subList结果不可强转成ArrayList，否则会抛出ClassCastException异常：java.util.RandomAccessSubList cannot be cast to java.util.ArrayList ;

> 说明：subList返回的是 ArrayList的内部类 SubList，并不是 ArrayList，而是ArrayList的一个视图，对于SubList子列表的所有操作最终会反映到原列表上。

3.\*\*【强制】\*\*在subList场景中，高度注意对原集合元素个数的修改，会导致子列表的遍历、增加、删除均产生ConcurrentModificationException异常。

4.\*\*【强制】\*\*使用集合转数组的方法，必须使用集合的toArray\(T\[\] array\)，传入的是类型完全一样的数组，大小就是list.size\(\)。

```text
反例：直接使用toArray无参方法存在问题，此方法返回值只能是Object[]类，若强转其它类型数组将出现ClassCastException错误。
正例：
List<String> list = new ArrayList<String>(2);
list.add("guan");
list.add("bao");
String[] array = new String[list.size()];
array = list.toArray(array);
说明：使用toArray带参方法，入参分配的数组空间不够大时，toArray方法内部将重新分配
内存空间，并返回新数组地址；如果数组元素大于实际所需，下标为[ list.size() ]的数组
元素将被置为null，其它数组元素保持原值，因此最好将方法入参数组大小定义与集合元素
个数一致。
```

5.\*\*【强制】\*\*使用工具类Arrays.asList\(\)把数组转换成集合时，不能使用其修改集合相关的方法，它的add/remove/clear方法会抛出UnsupportedOperationException异常。

> 说明：asList的返回对象是一个Arrays内部类，并没有实现集合的修改方法。Arrays.asList体现的是适配器模式，只是转换接口，后台的数据仍是数组。

```text
String[] str = new String[] { "a", "b" };
List list = Arrays.asList(str);
第一种情况：list.add("c");运行时异常。
第二种情况：str[0]= "gujin";那么list.get(0)也会随之修改。
```

6.\*\*【强制】\*\*泛型通配符&lt;? extends T&gt;来接收返回的数据，此写法的泛型集合不能使用add方法。

> 说明：苹果装箱后返回一个&lt;? extends Fruits&gt;对象，此对象就不能往里加任何水果，包括苹果。

7.\*\*【强制】\*\*不要在foreach循环里进行元素的remove/add操作。remove元素请使用Iterator方式，如果并发操作，需要对Iterator对象加锁。

```text
反例：
List<String> a = new ArrayList<String>();
	a.add("1");
	a.add("2");
	for (String temp : a) {
		if("1".equals(temp)){
		a.remove(temp);
		}
	}
	说明：以上代码的执行结果肯定会出乎大家的意料，那么试一下把“1”换成“2”，会是同样的
	结果吗？
	正例：
	Iterator<String> it = a.iterator();
	while(it.hasNext()){
		String temp = it.next();
		if(删除元素的条件){
		it.remove();
	}
}
```

8.\*\*【强制】\*\*在 JDK7版本以上，Comparator要满足自反性，传递性，对称性，不然Arrays.sort，Collections.sort会报IllegalArgumentException异常。

> 说明：

> 1）自反性：x，y的比较结果和y，x的比较结果相反。

> 2）传递性：x&gt;y,y&gt;z,则x&gt;z。

> 3）对称性：x=y,则x,z比较结果和y，z比较结果相同。

```text
反例：下例中没有处理相等的情况，实际使用中可能会出现异常：
new Comparator<Student>() {
	@Override
	public int compare(Student o1, Student o2) {
		return o1.getId() > o2.getId() ? 1 : -1;
	}
}
```

9.\*【推荐】\*集合初始化时，尽量指定集合初始值大小。

> 说明：ArrayList尽量使用ArrayList\(int initialCapacity\)初始化。

10.\*【推荐】\*使用entrySet遍历Map类集合KV，而不是keySet方式进行遍历。

> 说明：keySet其实是遍历了2次，一次是转为Iterator对象，另一次是从hashMap中取出key所对应的value。而entrySet只是遍历了一次就把key和value都放到了entry中，效率更高。如果是JDK8，使用Map.foreach方法。

```text
正例：values()返回的是V值集合，是一个list集合对象；keySet()返回的是K值集合，是一个Set集合对象；entrySet()返回的是K-V值组合集合。
```

11.\*【推荐】\*高度注意Map类集合K/V能不能存储null值的情况，如下表格：

| 集合类 | Key | Value | Super | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| Hashtable | 不允许为null | 不允许为null | Dictionary | 线程安全 |
| ConcurrentHashMap | 不允许为null | 不允许为null | AbstractMap | 分段锁技术 |
| TreeMap | 不允许为null | 允许为null | AbstractMap | 线程不安全 |
| HashMap | 允许为null | 允许为null | AbstractMap | 线程不安全 |

```text
反例：由于HashMap的干扰，很多人认为ConcurrentHashMap是可以置入null值，注意存储null值时会抛出NPE异常。
```

12.【参考】合理利用好集合的有序性\(sort\)和稳定性\(order\)，避免集合的无序性\(unsort\)和不稳定性\(unorder\)带来的负面影响。

> 说明：稳定性指集合每次遍历的元素次序是一定的。有序性是指遍历的结果是按某种比较规则依次排列的。如：ArrayList是order/unsort；HashMap是unorder/unsort；TreeSet是order/sort。

13.【参考】利用Set元素唯一的特性，可以快速对一个集合进行去重操作，避免使用List的contains方法进行遍历、对比、去重操作。

