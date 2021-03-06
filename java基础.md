[TOC]



## 1. 常量
用`final`修饰，一旦定义后面就不能修改了，如`final double MAX_D = 100.101`

定义一个类常量：在一个类中多个方法都能调用的常量
用`static final` 修饰

```java
public class Lei{
    public static final int AAA = 10;
    
    public static void main(){ int a = AAA }
    public static void method(){ int b = AAA }
}
```

## 2. 运算符

### 2.1. 异或（XOR，^）：不同为1，相同为0。

特殊用法：使特定数位翻转（与1异或）、保留原值（与0异或）、交换两个变量的值。

 交换两个变量的值：
- 借助第三个变量来实现。`C=A;A=B;B=C`;
- 利用加减法实现两个变量的交换。`A=A+B;B=A-B;A=A-B`;
- 用位异或运算来实现，效率最高。`A=A^B;B=A^B;A=A^B`;(==一个数异或本身等于0==)


### 2.2. 负数以其正值的补码形式表示

原码：一个整数按照绝对值大小转换成的二进制数称为原码。

`[+1]原= 0000 0001`

`[-1]原= 1000 0001`

反码：将二进制按位取反，所得的新二进制数称为原二进制数的反码。

`[+1] = [0000 0001]原= [0000 0001]反`

`[-1] = [1000 0001]原= [1111 1110]反`

补码的表示方法是，正数的补码就是其本身，负数的补码是在其原码的基础上，符号位不变，其余各位取反，最后+1（也就是在其反码的基础上+1）

`[+1] = [0000 0001]原= [0000 0001]反= [0000 0001]补`

`[-1] = [1000 0001]原= [1111 1110]反= [1111 1111]补`


### 2.3. 左移运算：value<<num

1）数值value向左移动num位，左边二进制位丢弃，右边补0。（注意byte和short类型移位运算时会变成int型，结果要强制转换）

2）若1被移位到最左侧，则变成负数。

3）左移时舍弃位不包含1，则左移一次，相当于乘2。

### 2.4. 右移运算：value>>num

1）数值value向右移动num位，正数左补0，负数左补1，右边舍弃。（即保留符号位）

2）右移一次，相当于除以2，并舍弃余数。

3）无符号右移>>>：左边位用0补充，右边丢弃

-5换算成二进制： `1111 1111 1111 1111 1111 1111 1111 1011`

-5右移3位后结果为-1，-1的二进制为：  `1111 1111 1111 1111 1111 1111 1111 1111`   // (用1进行补位)

-5无符号右移3位后的结果 536870911 换算成二进制：  `0001 1111 1111 1111 1111 1111 1111 1111`   // (用0进行补位)


### 2.5 运算符优先级

| 优先级 | 运算符                                             | 结合性   |
| ------ | -------------------------------------------------- | -------- |
| 1      | ()、[]、{}                                         | 从左向右 |
| 2      | !、+(一元运算符)、-、~、++、--                     | 从右向左 |
| 3      | *、/、%                                            | 从左向右 |
| 4      | +、-                                               | 从左向右 |
| 5      | <<、>>、>>>                                        | 从左向右 |
| 6      | <、<=、>、>=、instanceof                           | 从左向右 |
| 7      | ==、!=                                             | 从左向右 |
| 8      | &                                                  | 从左向右 |
| 9      | ^                                                  | 从左向右 |
| 10     | \|                                                 | 从左向右 |
| 11     | &&                                                 | 从左向右 |
| 12     | \|\|                                               | 从左向右 |
| 13     | ?:                                                 | 从右向左 |
| 14     | =、+=、-=、*=、/=、&=、\|=、^=、~=、<<=、>>=、>>>= | 从右向左 |

```java
int n=7; n<<=3; 

n=n & n + 1 | n + 2 ^ n + 3; 
// 先+ - 运算：n = 56 & 57 | 58 ^ 59  
// 然后 按照 & ^ | 顺序运算
n>>=2;
```

## 3. 字符串

### 3.1 子串
```java
String str = "hello";
String substr = str.substring(0,3);  // 从0到2的子串: hel
```

### 3.2 拼接
```java
        String a = "Hello";
        String b = "world";
        String c = a + b;   // 变量通过 +号 拼接
        String d = "hello " + b;  // 字符串 + 变量
        System.out.println("Hei "+ b);   // 在输出时通过 +号 拼接
        String all = String.join("/", "M","L","XL","XXL"); // 第一个为分隔符：M/L/XL/XXL
```

### 3.3 拆分split
`split() `方法根据匹配给定的正则表达式来拆分字符串。

注意：` . 、 $、 | 和 *` 等转义字符，必须得加 `\\`。

注意：多个分隔符，可以用 `|` 作为连字符。

```java
        a = "ab,bc,cd-d-e";
        b = "192.168.10.1";
        
        String[] al = a.split(",|-");
        for(String tmp1: al) System.out.println(tmp1);  
        
        for(String tmp2: b.split("\\.")) System.out.println(tmp2);
```

- `toLowerCase()` 转化为小写
- `toUpperCase()` 转化为大写
- `trim()` 删除首尾空格
- 

### 3.4 通过StringBuilder构建

#### 3.4.1 StringBuilder --> String
避免拼接很多小的字符串都要声明一个String来存储，浪费时空。
通过StringBuilder构建更快相当于放入缓存，当使用toString()方法时才声明一个String。
```java
        StringBuilder builder = new StringBuilder();  // 构建StringBuilder
        builder.append(a);       // 对其操作
        builder.append("abcd");
        
        String str1 = builder.toString();  // 生成一个String类
        
        System.out.println(str1);
        builder.insert(1,"hhh");
        String str2 = builder.toString();
        System.out.println(str2);
        builder.delete(2,5);
        String str3 = builder.toString();
        System.out.println(str3);
```

#### 3.4.2 字符串逆转
- `StringBuilder`有一个`reverse()`方法可以逆转字符串，但是`String`类没有该方法

#### 3.4.3 String --> StringBuilder
通过构造方法：`StringBuilder(String str)`
```java
        String s1 = "haha";
        StringBuilder s2 = new StringBuilder(s1);  // 构造时转变
        s2.reverse();    // 逆转字符串
        System.out.println(s2);
```

### 3.5 字符串比较`==`和`equals`

- `==`比较的是两个字符串的地址是否相同
- `equals`比较的是两个字符串的对象是否相同

```java
// new的数值在堆中，开辟了两个新的地址来存储，所以==比较不同
    String a = new String("aaaa");
    String b = new String("aaaa");
    System.out.println("a==b: " + (a==b));  // false
    System.out.println("a.equals(b): "+ a.equals(b)); // true
    
// 除了堆栈外有个常量池，字符串放入常量池，第一个写入，第二个相同的直接将地址引用相同的，所以==相同
    String a = "aaaaa";
    String b = "aaaaa";
    String c = a;      // 此时==得到的为true，指向同一个地址 
    System.out.println("a==b: "+ (a==b));  // true
    System.out.println("a.equals(b): "+ a.equals(b));  // true
```

## 4. ArrayList集合

- 什么是集合

提供一种存储空间可变的存储模型，存储的数据容量可以发生改变
- ArrayList 集合的特点

底层是数组实现的，长度可以变化
- 泛型的使用

用于约束集合中存储元素的数据类型

### 4.1 常用方法
| 方法名                               | 说明                                   |
| ------------------------------------ | -------------------------------------- |
| public boolean remove(Object o)      | 删除指定的元素，返回删除是否成功       |
| public E remove(int index)           | 删除指定索引处的元素，返回被删除的元素 |
| public E set(int index,E element)    | 修改指定索引处的元素，返回被修改的元素 |
| public E get(int index)              | 返回指定索引处的元素                   |
| public int size()                    | 返回集合中的元素的个数                 |
| public boolean add(E e)              | 将指定的元素追加到此集合的末尾         |
| public void add(int index,E element) | 在此集合中的指定位置插入指定的元素     |
```java
        ArrayList<String> as1 = new ArrayList<>();  // 声明集合类型为String类型
        as1.add("hahah");   // 添加默认放最后
        as1.add(s1);
        String s3 = as1.get(1);  // 获取集合元素
        System.out.println(s3);
        if ( as1.remove("hahah")) as1.add(0,"gai");  // remove删除元素，add(index, element) 添加至指定位置
        as1.set(1,"ahaha");  // 替换原有元素

        for (int i = 0; i < as1.size(); i++) {  // size()获取大小,遍历集合
            System.out.println(as1.get(i));
        }
```

### 4.2 初始化的几种方式
- 法一：asList
```java
ArrayList<T> obj = new ArrayList<T>(Arrays.asList(Object o1, Object o2, Object o3, ....so on));
```
- 法二：匿名内部类
```java
ArrayList<T> obj = new ArrayList<T>() {{
    add(Object o1);
    add(Object o2);
    ...
    ...
}};
```
- 法三：传统初始化
```java
ArrayList<T> obj = new ArrayList<T>();
obj.add("o1");
obj.add("o2");
...
...

// 或者
ArrayList<T> obj = new ArrayList<T>();
List list = Arrays.asList("o1","o2",...);
obj.addAll(list);
```
- 法四：指定初始化的元素个数和值
```java
ArrayList<T> obj = new ArrayList<T>(Collections.nCopies(count,element));
//把element复制count次填入ArrayList中
```

### 4.3 List初始化
```java
int[] intArray = new int[]{1, 2, 3};
Integer[] integerArray = new Integer[]{1, 2, 3};
 
List<int[] > intArrayList = Arrays.asList(intArray);  // 直接将数组转化list
List<Integer> integerList = Arrays.asList(integerArray); 
List<Integer> integerList2 = Arrays.asList(1, 2, 3);  // 直接数值初始化成list
List<String> stringList = Arrays.asList("a", "b", "c");  // 直接字符初始化为list
```

### 4.4 Arrays排序
通过方法`sort(T[] a, Comparator<? super T> c)`，设置比较器
```java
    String[] ss = {"a","ddd","bbbb","cc"};
    System.out.println(Arrays.toString(ss)); // [a, ddd, bbbb, cc]

    Arrays.sort(ss); // 默认排序按照ASCII码排序
    System.out.println(Arrays.toString(ss)); // [a, bbbb, cc, ddd]

    Arrays.sort(ss, (a,b) -> a.length()-b.length()); // 通过lambda实现Compareto接口以实现按照字符串长度排序
    System.out.println(Arrays.toString(ss)); // [a, cc, ddd, bbbb]
```
```java
    ArrayList<String> arr = new ArrayList<String>(Arrays.asList("bbbb","a","ddd","cc"));
    System.out.println(arr);  // [bbbb, a, ddd, cc]
    Collections.sort(arr, (a,b)->a.length() - b.length());
    System.out.println(arr);  // [a, cc, ddd, bbbb]
```

## 5. 集合

集合类型分为`Collection`和`Map`两大类
![image](http://c.biancheng.net/uploads/allimg/191205/5-1912051036333V.png)
![Map](http://c.biancheng.net/uploads/allimg/191205/5-191205103G5960.png)

Collection集合的常用方法
```java
//创建Collection集合的对象
Collection<String> c = new ArrayList<String>();
```
| 方法名                     | 说明                               |
| -------------------------- | ---------------------------------- |
| boolean add(E e)           | 添加元素                           |
| boolean remove(Object o)   | 从集合中移除指定的元素             |
| void clear()               | 清空集合中的元素                   |
| boolean contains(Object o) | 判断集合中是否存在指定的元素       |
| boolean isEmpty()          | 判断集合是否为空                   |
| int size()                 | 集合的长度，也就是集合中元素的个数 |

### 5.1 列表List

- List集合概述和特点
- List集合概述
    - ==有序==集合(也称为序列)，用户可以精确控制列表中每个元素的插入位置。用户可以通过整数索引访问元素，并搜索列表中的元素
    - 与Set集合不同，列表通常==允许重复==的元素
- List集合特点
    - 有索引
    - 可以存储重复元素
    - 元素存取有序

| 方法名                        | 描述                                   |
| ----------------------------- | -------------------------------------- |
| void add(int index,E element) | 在此集合中的指定位置插入指定的元素     |
| E remove(int index)           | 删除指定索引处的元素，返回被删除的元素 |
| E set(int index,E element)    | 修改指定索引处的元素，返回被修改的元素 |
| E get(int index)              | 返回指定索引处的元素                   |


```java
// 声明
List<Student> list = new ArrayList<Student>();

//迭代器：集合特有的遍历方式
Iterator<Student> it = list.iterator();
while (it.hasNext()) {
    Student s = it.next();
    System.out.println(s.getName()+","+s.getAge());
}

//普通for：带有索引的遍历方式
for(int i=0; i<list.size(); i++) {
    Student s = list.get(i);
    System.out.println(s.getName()+","+s.getAge());
}

//增强for：最方便的遍历方式
for(Student s : list) {
    System.out.println(s.getName()+","+s.getAge());
}
```

#### 5.1.1 List实现类ArrayList

- ArrayList集合
    - 底层是数组结构实现，查询快、增删慢
- LinkedList集合
    - 底层是链表结构实现，查询慢、增删快

`ArrayList`类包含Collection类的所有方法，还有常用的方法
表 1 ArrayList类的常用方法
| 方法名称                                    | 说明                                                         |
| ------------------------------------------- | ------------------------------------------------------------ |
| E get(int index)                            | 获取此集合中指定索引位置的元素，E 为集合中元素的数据类型     |
| int index(Object o)                         | 返回此集合中第一次出现指定元素的索引，如果此集合不包含该元素，则返回 -1 |
| int lastIndexOf(Object o)                   | 返回此集合中最后一次出现指定元素的索引，如果此集合不包含该元素，则返回 -1 |
| E set(int index, Eelement)                  | 将此集合中指定索引位置的元素修改为 element 参数指定的对象。此方法返回此集合中指定索引位置的原元素 |
| List<E> subList(int fromlndex, int tolndex) | 返回一个新的集合，新集合中包含 fromlndex 和 tolndex 索引之间的所有元素。包含 fromlndex 处的元素，不包含 tolndex 索引处的元素 |

`LinkedList`包含Collection方法，还有特有方法
| 方法名                    | 说明                             |
| ------------------------- | -------------------------------- |
| public void addFirst(E e) | 在该列表开头插入指定的元素       |
| public void addLast(E e)  | 将指定的元素追加到此列表的末尾   |
| public E getFirst()       | 返回此列表中的第一个元素         |
| public E getLast()        | 返回此列表中的最后一个元素       |
| public E removeFirst()    | 从此列表中删除并返回第一个元素   |
| public E removeLast()     | 从此列表中删除并返回最后一个元素 |


### 5.2 Set集合

- Set集合的特点
    - 元素存取无序
    - 没有索引、只能通过迭代器或增强for循环遍历
    - 不能存储重复元素
- 哈希值【理解】
    - 哈希值简介
        - 是JDK根据对象的地址或者字符串或者数字算出来的int类型的数值
    - 如何获取哈希值
        - Object类中的public int hashCode()：返回对象的哈希码值
    - 哈希值的特点
        - 同一个对象多次调用hashCode()方法返回的哈希值是相同的
        - 默认情况下，不同对象的哈希值是不同的。而重写hashCode()方法，可以实现让不同对象的哈希值相同
- HashSet集合的特点
    - 底层数据结构是哈希表
    - 对集合的迭代顺序不作任何保证，也就是说不保证存储和取出的元素顺序一致
    - 没有带索引的方法，所以不能使用普通for循环遍历
    - 由于是Set集合，所以是不包含重复元素的集合
- HashSet集合保证元素唯一性

![image](https://note.youdao.com/yws/public/resource/9a17bf7311b3424a6840aae93c5a8648/xmlnote/01190DAD843A4320950BE50559F86927/19474)
- 数据结构之哈希表
![image](https://note.youdao.com/yws/public/resource/9a17bf7311b3424a6840aae93c5a8648/xmlnote/4EBC952395EA4AA585FB91B7E7C448C3/19478)

- LinkedHashSet集合特点
    - 哈希表和链表实现的Set接口，具有可预测的迭代次序
    - 由链表保证元素有序，也就是说元素的存储和取出顺序是一致的
    - 由哈希表保证元素唯一，也就是说没有重复的元素
- TreeSet集合概述
    - 元素有序，可以按照一定的规则进行排序，具体排序方式取决于构造方法
        - TreeSet()：根据其元素的自然排序进行排序
        - TreeSet(Comparator comparator) ：根据指定的比较器进行排序
    - 没有带索引的方法，所以不能使用普通for循环遍历
    - 由于是Set集合，所以不包含重复元素的集合
```java
// 方法一： 在定义学生类时实现Comparable类并重写compareTo方法实现按照比较器排序
public class Student implements Comparable<Student> {
    private int age;
    
    @Override
    public int compareTo(Student s) {
// return 0;  返回0则不比较
// return 1;
// return -1;
//按照年龄从小到大排序
    int num = this.age - s.age;  this.age代表后面的值，从小到大排序
// int num = s.age - this.age;
//年龄相同时，按照姓名的字母顺序排序
    int num2 = num==0?this.name.compareTo(s.name):num;
    return num2;
    }
}
```

```java
// 方法二： 就是让集合构造方法接收Comparator的实现类对象，重写compare(T o1,T o2)方法
public static void main(String[] args) {
    //创建集合对象时，在构造方法中通过匿名类重写compare方法
    TreeSet<Student> ts = new TreeSet<Student>( new Comparator<Student>() {
    @Override
    public int compare(Student s1, Student s2) {
    //this.age - s.age
    //s1,s2
    int num = s1.getAge() - s2.getAge();
    int num2 = num == 0 ? s1.getName().compareTo(s2.getName()): num;
    return num2;
        }
    });

...
}

```


### 5.3 Map

- Map集合的特点
    - 键值对映射关系
    - 一个键对应一个值
    - 键不能重复，值可以重复
    - 元素存取无序
    - HashMap和TreeMap子类

| 方法名                              | 说明                                 |
| ----------------------------------- | ------------------------------------ |
| V put(K key,V value)                | 添加元素                             |
| V remove(Object key)                | 根据键删除键值对元素                 |
| void clear()                        | 移除所有的键值对元素                 |
| boolean containsKey(Object key)     | 判断集合是否包含指定的键             |
| boolean containsValue(Object value) | 判断集合是否包含指定的值             |
| boolean isEmpty()                   | 判断集合是否为空                     |
| int size()                          | 集合的长度，也就是集合中键值对的个数 |

| 获取的相关方法                 | 说明                     |
| ------------------------------ | ------------------------ |
| V get(Object key)              | 根据键获取值             |
| Set keySet()                   | 获取所有键的集合         |
| Collection values()            | 获取所有值的集合         |
| Set<Map.Entry<K,V>> entrySet() | 获取所有键值对对象的集合 |

```java
// 常用的遍历Map集合方法：
// 方法一：通过keySet获取所有键，根据get获取相应的值
Set<String> keySet = map.keySet();
//遍历键的集合，获取到每一个键。用增强for实现
for (String key : keySet) {
//根据键去找值。用get(Object key)方法实现
    String value = map.get(key);
    System.out.println(key + "," + value);
}
// 方法二：通过entrySet()获取键值对
Set<Map.Entry<String, String>> entrySet = map.entrySet();
//遍历键值对对象的集合，得到每一个键值对对象
for (Map.Entry<String, String> me : entrySet) {
//根据键值对对象获取键和值
    String key = me.getKey();
    String value = me.getValue();
    System.out.println(key + "," + value);
}

```

### 5.4 集合嵌套
```java
// ArrayList中嵌套HashMap
ArrayList< HashMap<String, String> > array = new ArrayList< HashMap<String, String> >();

// HashMap中嵌套ArrayList
HashMap<String, ArrayList<String>> hm = new HashMap<String, ArrayList<String>>();
```

### 5.5 Collections集合工具类
| 方法名                                   | 说明                               |
| ---------------------------------------- | ---------------------------------- |
| public static void sort(List list)       | 将指定的列表按升序排序             |
| public static void reverse(List<?> list) | 反转指定列表中元素的顺序           |
| public static void shuffle(List<?> list) | 使用默认的随机源随机排列指定的列表 |

## 6. 泛型

- 含义： 就是将类型由原来的具体的类型参数化，然后在使用/调用时传入具体的类型
- 使用： 这种参数类型可以用在类、方法和接口中，分别被称为泛型类、泛型方法、泛型接口

```java
// 1. 泛型类定义
public class Generic<T> {
    private T t;
    
    public T getT() {
        return t;
    }
    public void setT(T t) {
        this.t = t;
    }
}
// 实例化泛型
Generic<String> g1 = new Generic<String>();
Generic<Integer> g2 = new Generic<Integer>();

// 2. 泛型方法定义
public <T> void show(T t) {
    System.out.println(t);
}
g.show(30);
g.show(true);



// 3. 泛型接口定义
public interface Generic<T> {
    void show(T t);
}

public class GenericImpl<T> implements Generic<T> {
    @Override
    public void show(T t) {
        System.out.println(t);
    }
}
Generic<String> g1 = new GenericImpl<String>();
g1.show("林青霞");

```
## 7. 类型通配符
- 作用：表示各种泛型List的父类
- 类型通配符：<?>
    - List<?>：表示元素类型未知的List，它的元素可以匹配任何的类型
    - 这种带通配符的List仅表示它是各种泛型List的父类，并不能把元素添加到其中
- 类型通配符上限：<? extends 类型>
    - 例如： List<? extends Number>：它表示的类型是Number或者其子类型Integer
- 类型通配符下限：<? super 类型>
    - 例如： List<? super Number>：它表示的类型是Number或者其父类型Object

## 8. 可变参数
`int... a`表示，多个变量时可变参数放最后：`int b, int... a`

```java
public static int sum(int... a) {
    int sum = 0;
    for(int i : a) { sum += i; }
    return sum;
}
```

## 9. IO文件

### 9.1 File

#### 9.1.1 File基本介绍声明
- File类介绍
    - 它是文件和目录路径名的抽象表示
    - 文件和目录是可以通过File封装成对象的
    - 对于File而言，其封装的并不是一个真正存在的文件，仅仅是一个路径名而已。它可以是存在的，==也可以是不存在的==。将来是要通过具体的操作把这个路径的内容转换为具体存在的
    
| 方法名                            | 说明                                                        |
| --------------------------------- | ----------------------------------------------------------- |
| File(String pathname)             | 通过将给定的路径名字符串转换为抽象路径名来创建新的 File实例 |
| File(String parent, String child) | 从父路径名字符串和子路径名字符串创建新的File实例            |
| File(File parent, String child)   | 从父抽象路径名和子路径名字符串创建新的 File实例             |

示例：`File f1 = new File("E:\\itcast\\java.txt");`

#### 9.1.2 常用创建功能方法
| 方法名                         | 说明                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| public boolean createNewFile() | 当具有该名称的文件不存在时，创建一个由该抽象路径名命名的新空文件 |
| public boolean mkdir()         | 创建由此抽象路径名命名的目录                                 |
| public boolean mkdirs()        | （创建多级不存在目录）创建由此抽象路径名命名的目录，包括任何必需但不存在的父目录 |

`File f4 = new File("E:\\itcast\\javase.txt");System.out.println(f4.mkdir());`

此时能够创建一个文件夹为`javase.txt`的目录

#### 9.1.3 判断和获取功能
- 判断功能

| 方法名                       | 说明                                 |
| ---------------------------- | ------------------------------------ |
| public boolean isDirectory() | 测试此抽象路径名表示的File是否为目录 |
| public boolean isFile()      | 测试此抽象路径名表示的File是否为文件 |
| public boolean exists()      | 测试此抽象路径名表示的File是否存在   |

- 获取功能

| 方法名                          | 说明                                                     |
| ------------------------------- | -------------------------------------------------------- |
| public String getAbsolutePath() | 返回此抽象路径名的绝对路径名字符串                       |
| public String getPath()         | 将此抽象路径名转换为路径名字符串                         |
| public String getName()         | 返回由此抽象路径名表示的文件或目录的名称                 |
| public String[] list()          | 返回此抽象路径名表示的目录中的文件和目录的名称字符串数组 |
| public File[] listFiles()       | 返回此抽象路径名表示的目录中的文件和目录的File对象数组   |

- 删除功能

`public boolean delete() `删除由此抽象路径名表示的文件或目录

#### 9.1.4 递归遍历输出当前目录下所有的文件名
```java
public static void getAllFileName(File f){
        File[] filelist = f.listFiles();  // 获取当前目录列表
        if(filelist != null){
            for(File e: filelist){
                if(e.isDirectory() ){  // 当当前目录下还含有文件夹的话继续递归遍历
                    getAllFileName(e);
                }else{
                    System.out.println(e.getName());  // 获取当前目录下的文件名称
                }
            }
        }
    }
```


### 9.2 I/O

![image](https://note.youdao.com/yws/public/resource/9a17bf7311b3424a6840aae93c5a8648/xmlnote/37C9590457C443619F5B19FB6C35781F/19903)
![image](https://note.youdao.com/yws/public/resource/9a17bf7311b3424a6840aae93c5a8648/xmlnote/C5BDC1ADEF884B9BA33FD739A4B26ED7/19904)

#### 9.2.1 常用方法
`FileOutputStream`常用方法，将指定字节写入文件中

| 方法名                                 | 说明                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| void write(int b)                      | 将指定的字节写入此文件输出流 一次写一个字节数据              |
| void write(byte[] b)                   | 将b.length字节从指定的字节数组写入此文件输出流一次写一个字节数组数据 |
| void write(byte[] b, int off, int len) | 将len字节从指定的字节数组开始，从偏移量off开始写入此文件输出流 一次写一个字节数组的部分数据 |
| void close()                           | 关闭数据流，当完成对数据流的操作之后需要关闭数据流           |

默认是覆盖源文件重新写入，如果源文件不存在则创建该文件并写入

通过`FileOutputStream fos = new FileOutputStream("myByteStream\\fos.txt",true);`在后面追加`true`后则为追加写入，而非覆盖源文件。


`FileInputStream`常用方法
| 名称                               | 作用                                                         |
| :--------------------------------- | :----------------------------------------------------------- |
| int read()                         | 从输入流读入一个 8 字节的数据，将它转换成一个 0~ 255的整数，返回一个整数，如果遇到输入流的结尾返回 -1 |
| int read(byte[] b)                 | 从输入流读取若干字节的数据保存到参数 b 指定的字节数组中，返回的字节数表示读取的字节数，如果遇到输入流的结尾返回 -1 |
| int read(byte[] b,int off,int len) | 从输入流读取若干字节的数据保存到参数 b 指定的字节数组中，其中 off 是指在数组中开始保存数据位置的起始下标，len 是指读取字节的位数。返回的是实际读取的字节数，如果遇到输入流的结尾则返回 -1 |
| void close()                       | 关闭数据流，当完成对数据流的操作之后需要关闭数据流           |

在==用完文件资源后一定要释放资源==：`fos.close()`或`fis.close()`

#### 9.2.2 异常处理
```java
FileOutputStream fos = null;
try {
    fos = new FileOutputStream("myByteStream\\fos.txt");
    fos.write("hello".getBytes());
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if(fos != null) {
        try {
            fos.close();   
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

#### 9.2.3 字节流读数据

1. 一次读一个字节数据
```java
    FileInputStream fis = new FileInputStream("myByteStream\\fos.txt");
    int by;
    /*
    fis.read()：读数据
    by=fis.read()：把读取到的数据赋值给by
    by != -1：判断读取到的数据是否是-1
    */
    while ((by=fis.read())!=-1) {
        System.out.print((char)by);
    }
    //释放资源
    fis.close();
```
2. 一次读一个字节数组数据，复制文件
```java
//根据数据源创建字节输入流对象
FileInputStream fis = new FileInputStream("E:\\itcast\\mn.jpg");
//根据目的地创建字节输出流对象
FileOutputStream fos = new FileOutputStream("myByteStream\\mn.jpg");
//读写数据，复制图片(一次读取一个字节数组，一次写入一个字节数组), 一般大小为1024*n
byte[] bys = new byte[1024];  
int len;
while ((len=fis.read(bys))!=-1) {
    fos.write(bys,0,len);
}
//释放资源
fos.close();
fis.close();
```

## 10. 字节字符缓冲流

### 10.1 字节缓冲流

- 字节缓冲流介绍
    - lBufferOutputStream：该类实现缓冲输出流。 通过设置这样的输出流，应用程序可以向底层输出流写入字节，而不必为写入的每个字节导致底层系统的调用
    - lBufferedInputStream：创建BufferedInputStream将创建一个内部缓冲区数组。 当从流中读取或跳过字节时，内部缓冲区将根据需要从所包含的输入流中重新填充，一次很多字节
    
| 方法名                                 | 说明                   |
| -------------------------------------- | ---------------------- |
| BufferedOutputStream(OutputStream out) | 创建字节缓冲输出流对象 |
| BufferedInputStream(InputStream in)    | 创建字节缓冲输入流对象 |

- 通过字节数组缓冲流复制数据：这种方式传输最快，相对单字节的缓冲流和字节数组的字节流来说
```java
    BufferedInputStream bis = new BufferedInputStream( new FileInputStream("D:\\temp\\a.exe") );
    BufferedOutputStream bos = new BufferedOutputStream( new FileOutputStream("D:\\temp\\a4.exe") );

    int len;
    byte[] bys = new byte[1024];
    while ( (len = bis.read(bys)) != -1 ){
        bos.write(bys, 0, len);
    }

    bos.close();
    bis.close();
```

### 10.2 字符流

#### 10.2.1 基本介绍
- 字符流的介绍
    - 由于字节流操作中文不是特别的方便，所以Java就提供字符流
    - 字符流 = 字节流 + 编码表
- 编码表
    - 什么是字符集：字符编码，有ASCII字符集、GBXXX字符集、Unicode字符集等 


字符串中的编码解码问题
| 方法名                                   | 说明                                               |
| ---------------------------------------- | -------------------------------------------------- |
| byte[] getBytes()                        | 使用平台的默认字符集将该 String编码为一系列字节    |
| byte[] getBytes(String charsetName)      | 使用指定的字符集将该 String编码为一系列字节        |
| String(byte[] bytes)                     | 使用平台的默认字符集解码指定的字节数组来创建字符串 |
| String(byte[] bytes, String charsetName) | 通过指定的字符集解码指定的字节数组来创建字符串     |

```java
    String a = "中国boy";

    byte[] bysUtf = a.getBytes();   // 默认UTF-8
    byte[] bysGbk = a.getBytes("GBK");  // 通过GBK编码，得到字节数组
    System.out.println(Arrays.toString(bysUtf)); // 输出字节数组
    System.out.println(Arrays.toString(bysGbk));

    String aUtf = new String(bysUtf,"UTF-8");  // 按照UTF-8格式解码成字符
    String aGbk = new String( bysGbk, "GBK" );
```

- 字节流是否可以取代字符流？字符流存在的意义？
    - 当对非英文字符操作时，读取文本操作时对于多种编码格式的文本非常有必要使用字符流
    - 如果对不同编码格式的文本仅仅是复制传输操作，而不进行识别后操作的话没有必要使用字符流，反而会增加编码解码时间
    - 例如读取中文文本后，将文本写入数据集中数据库中，将文本显示在输出框中则很有必要
    - 字符流的`BufferedReader`和`BufferedWriter`有一个特有的方法`readline`and`nextline`仅针对`UTF-8`默认格式的存在（因为只能通过`FileWriter`和`FileReader`声明，而它们只能使用默认格式）

#### 10.2.2 字符流中的编码解码问题
- InputStreamReader：它读取字节，并使用指定的编码将其解码为字符
- OutputStreamWriter：是从字符流到字节流的桥梁，使用指定的编码将写入的字符编码为字节
```java
    OutputStreamWriter osw2 = new OutputStreamWriter( new FileOutputStream("idea_demo\\java2.txt") ,"GBK2312");
    InputStreamReader isr2 = new InputStreamReader( new FileInputStream("idea_demo\\java.txt") ,"GBK2312");

    int len2;
    char[] chs2 = new char[1024];
    while( (len2 = isr2.read(chs2)) != -1 ){
        // osw2.write( new String(chs2, 0, len2));
        osw2.write( chs2, 0, len2 )
    }

    osw2.close();
    isr2.close();
```
| 方法名                                             | 说明                                         |
| -------------------------------------------------- | -------------------------------------------- |
| InputStreamReader(InputStream in)                  | 使用默认字符编码创建InputStreamReader对象    |
| InputStreamReader(InputStream in,String chatset)   | 使用指定的字符编码创建InputStreamReader对象  |
| OutputStreamWriter(OutputStream out)               | 使用默认字符编码创建OutputStreamWriter对象   |
| OutputStreamWriter(OutputStream out,Stringcharset) | 使用指定的字符编码创建OutputStreamWriter对象 |

- 字符流写数据的5种方式

| 方法名                                    | 说明                 |
| ----------------------------------------- | -------------------- |
| void write(int c)                         | 写一个字符           |
| void write(char[] cbuf)                   | 写入一个字符数组     |
| void write(char[] cbuf, int off, int len) | 写入字符数组的一部分 |
| void write(String str)                    | 写一个字符串         |
| void write(String str, int off, int len)  | 写一个字符串的一部分 |


- `close()` 关闭流，释放资源，但是在关闭之前会先刷新流。一旦关闭，就不能再写数据

- 字符流读数据

| 方法名                | 说明                   |
| --------------------- | ---------------------- |
| int read()            | 一次读一个字符数据     |
| int read(char[] cbuf) | 一次读一个字符数组数据 |


#### 10.2.3 字符缓冲流

- BufferedWriter：将文本写入字符输出流，缓冲字符，以提供单个字符，数组和字符串的高效写入，可以指定缓冲区大小，或者可以接受默认大小。默认值足够大，可用于大多数用途
- BufferedReader：从字符输入流读取文本，缓冲字符，以提供字符，数组和行的高效读取，可以指定缓冲区大小，或者可以使用默认大小。 默认值足够大，可用于大多数用途

| 方法名                     | 说明                   |
| -------------------------- | ---------------------- |
| BufferedWriter(Writer out) | 创建字符缓冲输出流对象 |
| BufferedReader(Reader in)  | 创建字符缓冲输入流对象 |

- `BufferedWriter`特有方法：`void newLine()` 写一行行分隔符，行分隔符字符串由系统属性定义
- `BufferedReader`特有方法`String readLine()` 读一行文字。结果包含行的内容的字符串，不包括任何行终止字符如果流的结尾已经到达，则为`null`

```java
    BufferedReader br = new BufferedReader( new FileReader("D:\\temp\\aaa.txt") );
    BufferedWriter bw = new BufferedWriter( new FileWriter("D:\\temp\\aaa4.txt") );

    String line;
    int lens;
    while( (line = br.readLine()) != null ){
        bw.write(line2);
        bw.newLine();
        bw.flush();
    }
    
//  int blen;
//  char[] bchs = new char[1024];
//  while( (blen = br.read(bchs)) != -1){
//      bw.write( new String(bchs, 0 ,blen) );
//  }

    br.close();
    bw.close();
```

## 11. 特殊操作流

### 11.1 `Scanner`和`BufferedReader`的区别
- `Scanner`:解析基本数据类型和字符串。它本质上是使用正则表达式去读取不同的数据类型
- `BufferedReader`: 高效的读取字符序列，从字符输入流和字符缓冲区读取文本，读取固定一行`BufferedReader br = new BufferedReader (newInputStreamReader(System.in))`，返回字符串
- 两者对比
    1. `Scanner`提供了一系列`nextXxx()`方法，当我们确定输入的数据类型时，使用`Scanner`更加方便。也正是因为这个`BufferedReader`相对于`Scanner`来说要快一点，因为`Scanner`对输入数据进行类解析，而`BufferedReader`只是简单地读取字符序列。
    2. `Scanner`和`BufferedReader`都设置了缓冲区，`Scanner`有很少的缓冲区(1KB字符缓冲)相对于`BufferedReader`(8KB字节缓冲)，但是这是绰绰有余的。
    3. `BufferedReader`是支持同步的，而`Scanner`不支持。如果我们处理多线程程序，`BufferedReader`应当使用。
    4. `Scanner`输入的一个问题：在`Scanner`类中如果我们在任何7个nextXXX()方法之后调用`nextLine()`方法，这`nextLine()`方法不能够从控制台读取任何内容，并且，这游标不会进入控制台，它将跳过这一步。`nextXXX()`方法包括`nextInt()，nextFloat()， nextByte()，nextShort()，nextDouble()，nextLong()，next()`。在`BufferReader`类中就没有那种问题。这种问题仅仅出现在`Scanner`类中，由于`nextXXX()`方法忽略换行符，但是`nextLine()`并不忽略它。如果我们`在nextXXX()`方法和`nextLine()`方法之间使用超过一个以上的`nextLine()`方法，这个问题将不会出现了；因为`nextLine()`把换行符消耗了。

原文链接：https://blog.csdn.net/zengxiantao1994/article/details/78056243

```java
    // 通过BufferedReader方式读取数据
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    System.out.println(br.readLine());
    
    // 通过系统提供的Scanner方式
    Scanner sc = new Scanner(System.in);
    System.out.println(sc.nextInt());
    sc.nextLine();    // 必须要消耗一个nextLine，否则当输入第一个数字后按enter换行时直接结束，消耗了一个换行 
    System.out.println(sc.nextLine());
```

### 11.2 标准输入流

`public static final InputStream in` 用户键盘主机输入

`InputStream is = System.in`

`Scanner(InputStream source)`是Scanner的一种构造方法，使用的`Scanner(System.in)`

### 11.3 标准输出流
`PrintStream ps = System.out;`

`PrintStream`类的所有方法，`System.out`都可以使用，例如：`print()`/`printf()`/`println()`

### 11.4 字符打印流

| 方法名                                     | 说明                                                         |
| ------------------------------------------ | ------------------------------------------------------------ |
| PrintWriter(String fileName)               | 使用指定的文件名创建一个新的PrintWriter，而不需要自动执行刷新 |
| PrintWriter(Writer out, boolean autoFlush) | 创建一个新的PrintWriter out：字符输出流 autoFlush： 一个布尔值，如果为真，则println，printf，或format方法将刷新输出缓冲区 |

```java
    PrintWriter pw2 = new PrintWriter( new FileWriter("idea_demo\\java3.txt", true), true);   
    // 第一个true为添加写入文件，第二个true为自动刷新无需手动写pw.flush
    pw2.write("hellp");
    pw2.println(99); // 直接写入99
    pw2.write(99);  // 转换为字符 c 写入
    pw2.close();
```

### 11.5 对象序列化流

- 对象序列化介绍
    - 对象序列化：就是将对象保存到磁盘中，或者在网络中传输对象
    - 这种机制就是使用一个字节序列表示一个对象，该字节序列包含：对象的类型、对象的数据和对象中存储的属性等信息
    - 字节序列写到文件之后，相当于文件中持久保存了一个对象的信息
    - 反之，该字节序列还可以从文件中读取回来，重构对象，对它进行反序列化
- 对象序列化流： ObjectOutputStream
    - 将Java对象的原始数据类型和图形写入OutputStream。
    - 可以使用ObjectInputStream读取（重构）对象。
    - 可以通过使用流的文件来实现对象的持久存储。
    - 如果流是网络套接字流，则可以在另一个主机上或另一个进程中重构对象
- 构造方法

| 方法名                                | 说明                                               |
| ------------------------------------- | -------------------------------------------------- |
| Object OutputStream(OutputStream out) | 创建一个写入指定的OutputStream的ObjectOutputStream |
-  序列化对象的方法：`void writeObject(Object obj)`
- 对象反序列化：`Object InputStream(InputStream in)`创建从指定的`InputStream`读取的`ObjectInputStream`
- 对象反序列化方法:`Object readObject()` 从`ObjectInputStream`读取一个对象

```java
// 对象要实现Serializable接口以表示该类使用了对象序列化
    public class Student implements Serializable {
        private static final long serialVersionUID = 42L; 
        // 设定serialVersionUID为固定值，后面如果该对象发生改变也可以继续读取，否则如果该对象发生了一点点变化也无法读取成功，建议设定固定值
        private String name;
        private transient int age;  // 通过transient使得该变量不参与对象序列化
        public Student() {
        }
        ......
    }

    // 写入对象序列
    ObjectOutputStream oos = new ObjectOutputStream( new FileOutputStream("idea_demo\\java4.txt") );
    Student s1 = new Student("中国", 10,20,30);
    Student s2 = new Student("中国11", 10,20,32);
    oos.writeObject(s1);
    oos.writeObject(s2);
    oos.close();
    
    // 读取多个对象序列
    ObjectInputStream ois = new ObjectInputStream( new FileInputStream("idea_demo\\java4.txt") );
    Object obj = null;
    while (true){    // 读取多个对象
        try{
            Student ss = (Student)ois.readObject();
            System.out.println(ss.getName() + ":" + ss.getAge());  // 对于没有序列化的数据默认为0
        }catch (EOFException e){
            break;
        }catch (NullPointerException ee){
            continue;
        }
    }
    ois.close();
```

## 12 Properties集合

- Properties类继承自HashTable，通常和io流结合使用。
- 它最突出的特点是将key/value作为配置属性写入到配置文件中以实现配置持久化，或从配置文件中读取这些属性。
- 它的这些配置文件的规范后缀名为".properties"。表示了一个持久的属性集。

| 方法名                                        | 说明                                                         |
| --------------------------------------------- | ------------------------------------------------------------ |
| put(Object key, Object key)                   | 将指定的 key映射到此散列表中指定的 value                     |
| get(Object key)                               | 返回指定键映射到的值，如果此映射不包含键的映射，则返回 null  |
| Object setProperty(String key,String value)   | 设置集合的键和值，都是String类型，底层调用 Hashtable方法     |
| put String getProperty(String key)            | 使用此属性列表中指定的键搜索属性                             |
| Set stringPropertyNames()                     | 从该属性列表中返回一个不可修改的键集，其中键及其对应的值是字符串 |
| void load(InputStream inStream)               | 从输入字节流读取属性列表（键和元素对）                       |
| void load(Reader reader)                      | 从输入字符流读取属性列表（键和元素对）                       |
| void store(OutputStream out, String comments) | 将此属性列表（键和元素对）写入此 Properties表中，以适合于使用load(InputStream)方法的格式写入输出字节流 |
| void store(Writer writer, String comments)    | 将此属性列表（键和元素对）写入此Properties表中，以适合使用 load(Reader)方法的格式写入输出字符流 |

## 网络编程

### 13.1 `InetAddress`
```java
//InetAddress address = InetAddress.getByName("itheima");
InetAddress address = InetAddress.getByName("192.168.1.66");

//public String getHostName()：获取此IP地址的主机名
String name = address.getHostName();

//public String getHostAddress()：返回文本显示中的IP地址字符串
String ip = address.getHostAddress();
```

### 13.2 UDP通信
- `UDP`使用`DatagramSocket`创建接收和发送端的socket
- 使用`DatagramPacket`封装报文`DatagramPacket(byte[] buf, int length, InetAddress address, int port)`需要字节数组

```java
Send: 
    //1. 创建发送端的Socket对象(DatagramSocket)
    DatagramSocket ds = new DatagramSocket();
    
    //自己封装键盘录入数据
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    String line;
    while ((line = br.readLine()) != null) {
        //输入的数据是886，发送数据结束
        if ("886".equals(line)) {
        break;
        }
        //2. 创建数据，并把数据打包
        byte[] bys = line.getBytes();
        DatagramPacket dp = new DatagramPacket(bys, bys.length, InetAddress.getByName("192.168.1.66"), 12345);
        
        //3. 调用DatagramSocket对象的方法发送数据
        ds.send(dp);
    }
        
    //4. 关闭发送端
    ds.close();
```
```java
Receive: 
    //1. 创建接收端的Socket对象(DatagramSocket)
    DatagramSocket ds = new DatagramSocket(12345);
    
    while (true) {
        //2. 创建一个数据包，用于接收数据
        byte[] bys = new byte[1024];
        DatagramPacket dp = new DatagramPacket(bys, bys.length);
        
        //3. 调用DatagramSocket对象的方法接收数据
        ds.receive(dp);
        
        //4. 解析数据包
        System.out.println("数据是：" + new String(dp.getData(), 0,
        dp.getLength()));
    }
    ds.close()
```


### 13.3 TCP通信

- 客户端提供了`Socket`类，为服务器端提供了`ServerSocket`类并提供`accept()`方法接收`Socket`
- `Socket`类提供获取输入输出流来读取和发送数据

| 方法名                         | 说明                 |
| ------------------------------ | -------------------- |
| InputStream getInputStream()   | 返回此套接字的输入流 |
| OutputStream getOutputStream() | 返回此套接字的输出流 |

- 通过`OutputStream os = s.getOutputStream()`，然后`os.write( "haha".getByte() )`来发送数据
- 通过`InputStream is = s.getInputStream()`,然后`byte[] bys = new byte[1024]; int len = is.read(bys)`将数据读取到`bys`中
- 通过`BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));`，然后使用`br.readLine()`来逐行读取字符串
- 通过`BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));`,然后使用`bw.write(String), bw.newLine()`来发送字符串

#### 13.3.1 TCP基本使用过程
```java
TCPClient
    // 1. 创建客户端
    Socket s = new Socket("10.152.137.87",2000);

    // 2. 写数据
    OutputStream os = s.getOutputStream();
    os.write("hello tcp,你好 ！".getBytes());

    // 3. 接收反馈
    InputStream is = s.getInputStream();
    byte[] bys = new byte[1024];
    int len = is.read(bys);
    System.out.println("receive data: "+ new String(bys, 0, len));

    // 4. 释放资源
    s.close();
```
```java
TCPServer
    // 1. 声明服务端套接字
    ServerSocket ss = new ServerSocket(2000);

    // 2. 接收套接字，再转为字节流
    Socket s = ss.accept();
    InputStream is = s.getInputStream();
    byte[] bys = new byte[1024];
    int len = is.read(bys);
    System.out.println("receive for client: "+ new String(bys, 0, len));

    // 3. 反馈字节流
    OutputStream os = s.getOutputStream();
    os.write("hello client啊！".getBytes());

    // 4. 释放资源
    ss.close();
```

#### 13.3.2 TCP多线程对文本复制
```java
TCPClientTread
    Socket s = new Socket("10.152.137.87",20001);
    
    // 文本字节输入输出流,一个从文本读取，一个传输给套接字以输出
    BufferedReader br = new BufferedReader(new FileReader("idea_demo\\src\\java.txt")); 
    BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));

    String line;
    while( (line = br.readLine()) != null){
    // 文本输出三件套
        bw.write(line);
        bw.newLine();
        bw.flush();
    }

    // 当文件传输结束后，通过套接字特有方法shutdownOutput来传送终止连接信号
    s.shutdownOutput();
    
    // 接收反馈
    BufferedReader brClient = new BufferedReader(new InputStreamReader(s.getInputStream()));
    System.out.println("receive from server: " + brClient.readLine());

    // 关闭套接字，释放资源
    s.close();
    br.close();
```

```java
public class TcpServerRunable implements Runnable {
    private Socket s;

    public TcpServerRunable(Socket s) {
        this.s = s;
    }

    @Override
    public void run() {
        try {
        // 定义接收写入文本的方法
            BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));
            int count = 0;
            // 当文件存在时则重命名
            File f = new File("idea_demo\\src\\Network\\java[" + count + "].txt");
            while (f.exists()) {
                count++;
                f = new File("idea_demo\\src\\Network\\java[" + count + "].txt");
            }
            // 写入文本
            BufferedWriter bw = new BufferedWriter(new FileWriter(f));
            String line;
            // br.readLine逐行读取传入的字符串
            while ((line = br.readLine()) != null) {
                bw.write(line);
                bw.newLine();
                bw.flush();
            }

            BufferedWriter bwServer = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
            bwServer.write("load sucess!!!");
            bwServer.newLine();
            bwServer.flush();

            s.close();
            bw.close();

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}


public class TcpServerThread {
    public static void main(String[] args) throws IOException {
        ServerSocket ss = new ServerSocket(20001);
        while (true){
            new Thread( new TcpServerRunable(ss.accept()) ).start();
        }
    }
}

```


## 14 Lambda

### 14.1 前提和基本使用

- 使用前提：
    - 有一个接口
    - 接口中有且仅有一个抽象方法
- 使用方式:`(参数) -> {具体使用方法}`
- 省略模式
    - 参数类型可以省略。但是有多个参数的情况下，不能只省略一个
    - 如果参数有且仅有一个，那么小括号可以省略
    - 如果代码块的语句只有一条，可以省略大括号和分号，和 return关键字
```java
public interface Eatable {
    void eat();
}

public interface ReturnAndParam {
    int sum(int a, int b, String c);
}

public interface Param {
    void eat(int a);
}

public class EatableDemo {
    public static void main(String[] args) {
    
        useEatable( () -> { System.out.println("Running away"); } );
        useEatable( () -> System.out.println("Running away") ); // 只有一句方法体时可以省略{} 
        
        useParam( (int a) -> {System.out.println("Running away"); } );
        useParam( a -> System.out.println("Running away"); ); // 只有一个参数时，可以省略()和类型
    
        useReturnAndParam( (int a,int b,String c) -> {return a+b; } );    
        useReturnAndParam( (a,b,c) -> a+b );  // 可以同时省略参数类型，只有return一句时，可以省略return和{}
        
    }    
    
    public static void useEatable(Eatable e){
        e.eat();
    }
    
    public static void useParam(Param e){
        e.eat(a);
    }
    
    public static void useReturnAndParam(ReturnAndParam e){
        int sum = e.sum(10,20,"add");
        System.out.println(sum)
    }

}
```

### 14.2 Lambda表达式和匿名内部类的区别
- 所需类型不同
    - 匿名内部类：可以是接口，也可以是抽象类，还可以是具体类
    - Lambda 表达式：只能是接口
- 使用限制不同
    - 如果接口中有且仅有一个抽象方法，可以使用 Lambda表达式，也可以使用匿名内部类
    - 如果接口中多于一个抽象方法，只能使用匿名内部类，而不能使用 Lambda表达式
- 实现原理不同
    - 匿名内部类：编译之后，产生一个单独的 .class字节码文件
    - Lambda 表达式：编译之后，没有一个单独的.class字节码文件。对应的字节码会在运行的时候动态生成

## 15 方法引用

| 种类                   | 示例               | 说明                                                         | 对应lambda表达式                       |
| ---------------------- | ------------------ | ------------------------------------------------------------ | -------------------------------------- |
| 引用类方法             | 类名::类方法       | 函数式接口中被实现方法的全部参数传给该类方法作为参数         | (a,b,..) -> 类名.类方法(a,b,...)       |
| 引用特定对象的实例方法 | 特定对象::实例方法 | 函数式接口中被实现方法的全部参数传给该方法作为参数           | (a,b,..) -> 特定对象.实例方法(a,b,...) |
| 引用某类对象的实例方法 | 类名::实例方法     | 函数式接口中被实现方法的第一个参数作为调用者，后面的参数传给该方法作为参数 | (a,b,..) -> a.实例方法(a,b,...)        |
| 引用构造器             | 类名::new          | 函数式接口中被实现方法的全部参数传给该类方法作为参数         | (a,b,..) -> new 类名(a,b,...)          |

### 15.1 引用类方法（静态方法）
```java
public interface Mytest1 {
    int test(String s);
}

//  Mytest1 mt1 = a -> Integer.parseInt(a);  lambda方式
    Mytest1 mt1 = Integer::parseInt;  // 静态方法
    Integer inta = mt1.test("100");
    System.out.println(inta);
```

### 15.2 引用特定对象的实例方法
```java
public interface Mytest1 {
    int test(String s);
}

//  Mytest1 mt2 = a -> "This is special".indexOf(a);  
    Mytest1 mt2 = "This is special"::indexOf; // 特定对象："This is .."的实例方法indexOf(String)
    int intb = mt2.test("is");
    System.out.println(intb);
```

### 15.3 引用类对象的实例方法
```java
public interface Mytest {
    String test(String a,int b, int c);
}

public class MytestDemo {
    public static void main(String[] args) {
//        Mytest mt = (a,b,c) -> a.substring(b,c);  lambda实现方式
        Mytest mt = String::substring;  // 先创建对象，引用该对象的实例方法

        String str = mt.test("abcdefg", 2,4);
        System.out.println(str);
    }
}

```


### 15.4 引用构造器
```java
public class Student {
    private int age;
    private String name;

    public Student(String name, int age) {
        this.age = age;
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public String getName() {
        return name;
    }
}

public interface StudentBuilder {
    Student build(String name, int age);
}


//        StudentBuilder sb = (a,b) -> new Student(a,b);
        StudentBuilder sb = Student::new;  
        Student sd = sb.build("haha", 10);
        System.out.println(sd.getName()+":"+sd.getAge());

```


## 16 接口组成成员

- 常量：`public static final`
- 抽象方法:`public abstract`,通常直接写`void method();`默认省略了`public abstract`
- 默认方法（java 8）：`public default`，用于在已经写好的程序中如果增加接口的一个方法，就要在实现接口的所有类中重写添加该方法。添加默认方法可以直接在接口中实现该方法体，且所有实现该接口的类中无需做任何改变。
- 静态方法（Java 8）：`public static`，在实现类中调用静态方法，需要通过接口调用，避免继承多接口时有重复的方法名。
- 私有方法（Java 9）：`private `，仅供内部使用，当内部的多个方法有重复的实现时，可以抽象出一个私有方法，供内部使用，但是不想让外部调用。
    - 默认方法可以调用私有的静态方法和非静态方法
    - 静态方法只能调用私有的静态方法

# 17 Stream流
使用Stream流对集合数据操作，先将集合数据转化为流数据，然后对流数据操作，最后也可以转化为集合数据

## 17.1 生成Stream流
```java
    //Collection体系的集合可以使用默认方法stream()生成流
    List<String> list = new ArrayList<String>();
    Stream<String> listStream = list.stream();
    Set<String> set = new HashSet<String>();
    Stream<String> setStream = set.stream();
    
    //Map体系的集合间接的生成流
    Map<String,Integer> map = new HashMap<String, Integer>();
    Stream<String> keyStream = map.keySet().stream();
    Stream<Integer> valueStream = map.values().stream();
    Stream<Map.Entry<String, Integer>> entryStream = map.entrySet().stream();
    
    //数组可以通过Stream接口的静态方法of(T... values)生成流
    String[] strArray = {"hello","world","java"};
    Stream<String> strArrayStream = Stream.of(strArray);
    Stream<String> strArrayStream2 = Stream.of("hello", "world", "java");
    Stream<Integer> intStream = Stream.of(10, 20, 30);
```

## 17.2 Stream流操作
| 方法名                                   | 说明                                                       |
| ---------------------------------------- | ---------------------------------------------------------- |
| void forEach(Consumer action)            | 对此流的每个元素执行操作                                   |
| long count()                             | 返回此流中的元素数                                         |
| Stream filter(Predicate predicate)       | 用于对流中的数据进行过滤                                   |
| Stream limit(long maxSize)               | 返回此流中的元素组成的流，截取前指定参数个数的数据         |
| Stream skip(long n)                      | 跳过指定参数个数的数据，返回由该流的剩余元素组成的流       |
| static Stream concat(Stream a, Stream b) | 合并a和b两个流为一个流                                     |
| Stream distinct()                        | 返回由该流的不同元素（根据Object.equals(Object) ）组成的流 |
| Stream sorted()                          | 返回由此流的元素组成的流，根据自然顺序排序                 |
| Stream sorted(Comparator comparator)     | 返回由该流的元素组成的流，根据提供的Comparator进行排序     |
| Stream map(Function mapper)              | 返回由给定函数应用于此流的元素的结果组成的流               |
| IntStream mapToInt(ToIntFunction mapper) | 返回一个IntStream其中包含将给定函数应用于此流的元素的结果  |

```java
        ArrayList<String> str = new ArrayList<String>(Arrays.asList("haha", "hello","hhhh","ahang"));
        
        str.stream().filter( s -> s.startsWith("h")).forEach(System.out::println);  
        // filter过滤后只有以h开头的字符串，forEach()对流中每个元素操作，可能会无序
        str.stream().filter( s -> s.startsWith("h") ).filter(s -> s.length() == 4).forEach(s -> System.out.println(s));
        
        str.stream().skip(1).limit(2).forEach(System.out::println);
        // skip跳过前几个， limit只保存前几个
        
        Stream<String> s1 = str.stream().skip(1);
        Stream<String> s2 = str.stream().limit(3);
        Stream.concat(s1, s2).forEach(System.out::println);  // concat合并两个流中元素，重复也存在
        Stream.concat(s1,s2).distinct().forEach(System.out::println);  // distinct去除重复的元素 

        str.stream().sorted().forEach(System.out::println); // 按照字符默认排序
        str.stream().sorted( (a,b) -> {           // 实现Comparetor接口
            int num1 = a.length() - b.length();
            int num2 = num1 == 0? a.compareTo(b) : num1;
            return num2;
        } ).forEach(System.out::println);
        
        ArrayList<String> list = new ArrayList<String> (Arrays.asList("10", "20", "40","9"));
        list.stream().map(s -> Integer.parseInt(s)).forEach(s -> System.out.println(s));
        list.stream().map(Integer::parseInt).forEach(System.out::println);
        int sum = list.stream().mapToInt(Integer::parseInt).sum();  
        // mapToInt()可以转化stream为IntStream，会有数字的相关方法
```

## 17.3 Stream流转化为集合
```java
    ArrayList<String> str = new ArrayList<String>(Arrays.asList("haha", "hello","hhhh","ahang"));
    Stream<String> strStream= str.stream().filter(s -> s.length() == 4);
    List<String> lists = strStream.collect(Collectors.toList());   // collect(Collectors.toList()) 转化Stream为List集合
    Set<String> sets = strStream.collect(Collectors.toSet());   // collect(Collectors.toSet()) 转化Stream为Set集合

    String[] names = {"haha,20", "ahang,30","kaka,23"};
    Stream<String> arrayStream = Stream.of(names);
    // collect( Collectors.toMap(Function keyMapper,Function valueMapper))转化Stream为map集合
    Map<String, Integer> map = arrayStream.collect( Collectors.toMap(s->s.split(",")[0], s-> Integer.parseInt(s.split(",")[1]))  );
    Set<String> keySet = map.keySet();
    for(String key: keySet){
        Integer value = map.get(key);
        System.out.println(key + ":" + value);
    }
```

> l 在忘记root密码的时候，可以这样 
>
> 以windows为例： 
>
> 关闭正在运行的MySQL服务。 
>
> 打开DOS窗口，转到mysql\bin目录。 
>
> 输入mysqld --skip-grant-tables 回车。--skip-grant-tables 的意思是启动MySQL服务的时候跳过权限表认证。 
>
> 再开一个DOS窗口（因为刚才那个DOS窗口已经不能动了），转到mysql\bin目录。 
>
> 输入mysql回车，如果成功，将出现MySQL提示符 >。 
>
> 连接权限数据库： use mysql; 。 
>
> 改密码：update user set password=password("123") where user="root";（别忘了最后加分号） 。 
>
> 刷新权限（必须步骤）：flush privileges;　。 
>
> 退出 quit。 
>
> 注销系统，再进入，使用用户名root和刚才设置的新密码123登录。