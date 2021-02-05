###### tags: `JAVA`
# 07. 多形（Polymorphism）
## 多形
當多個不同的類別繼承同一個父類別，父類別的操作都可以套用在子類別上。並可經由Override使每個類別的動作有所不同。

![](https://i.imgur.com/FkD0IcI.png)

```java
package kensetsu;

public class HololiveMember {

	public String name;
	
	public HololiveMember(String n) {
		name = n;
	}
	
	public void buildHouse(int n) {
		for (int i = 0; i < n; i++) {
			System.out.println("家を作った");
		}
	}

}
```
```java
package kensetsu;

public class AkukinMember extends HololiveMember {

	public int tara;
	
	public AkukinMember(String n, int tara) {
		super(n);
		this.tara = tara;
	}
	
	@Override
	public void buildHouse(int n) {
		for (int i = 0; i < n; i++) {
			System.out.println(name + "、家を作った<Akukin建設>");
		}
	}

}
```
```java
package kensetsu;

public class UsadaMember extends HololiveMember {

	public int ninjin;
	
	public UsadaMember(String n, int ninjin) {
		super(n);
		this.ninjin = ninjin;
	}
	
	@Override
	public void buildHouse(int n) {
		for (int i = 0; i < n; i++) {
			System.out.println(name + "、家を作った<兎田建設>");
		}
	}

}
```
### main範例1
![](https://i.imgur.com/p6JiL3f.png)
```java
package kensetsu;

public class Stream {

	public HololiveMember liver;
	
	public Stream(HololiveMember m) {
		liver = m;
	}
	
	public void startStream() {
		System.out.println("ホロ鯖をログインしました！");
		liver.buildHouse(2);
	}

	public static void main(String[] args) {
		AkukinMember a = new AkukinMember("湊あくあ", 1000);
		UsadaMember u = new UsadaMember("Moona", 100);
		Stream s1 = new Stream(a);
		Stream s2 = new Stream(u);
		s1.startStream();
		s2.startStream();
	}

}
```
```
ホロ鯖をログインしました！
湊あくあ、家を作った<Akukin建設>
湊あくあ、家を作った<Akukin建設>
ホロ鯖をログインしました！
Moona、家を作った<兎田建設>
Moona、家を作った<兎田建設>
```
### main範例2
![](https://i.imgur.com/ayAPnFX.png)
```java
package kensetsu;

public class Stream {
	
	public static void startStream(HololiveMember liver) {
		System.out.println("ホロ鯖をログインしました！");
		liver.buildHouse(2);
	}

	public static void main(String[] args) {
		AkukinMember a = new AkukinMember("湊あくあ", 1000);
		UsadaMember u = new UsadaMember("Moona", 100);
		Stream.startStream(a);
		Stream.startStream(u);
	}

}
```
## is-a關係
```java
HololiveMember a = new AkukinMember("湊あくあ", 1000);
HololiveMember u = new UsadaMember("Moona", 100);
```
上面敘述能成立是因為AkukinMember是一種HololiveMember，UsadaMember也是一種HololiveMember。

-----

那麼如果反過來：
```java
AkukinMember a = new HololiveMember("湊あくあ"); //complie error
UsadaMember u = new HololiveMember("Moona"); //complie error
```
因為HololiveMember不是一種AkukinMember也不是一種UsadaMember，所以都無法編譯。

-----

如果強制轉型：
```java
AkukinMember a = (AkukinMember)new HololiveMember("湊あくあ"); //ClassCastException
UsadaMember u = (UsadaMember)new HololiveMember("Moona"); //ClassCastException
```
會發生ClassCastException（類別扮演例外）因為HololiveMember根本無法扮演AkukinMember或UsadaMember

-----

```java
HololiveMember h = new AkukinMember("湊あくあ", 1000);
AkukinMember a = (AkukinMember)h;
```
這本身沒什麼問題，因為h原本就是參考AkukinMember的實例（instance）。

＊instance與object基本上是一樣意思XD

-----

但以下就有問題了：
```java
HololiveMember h = new AkukinMember("湊あくあ", 1000);
UsadaMember u = (UsadaMember)h; //ClassCastException
```
h是參考AkukinMember的物件，不能扮演UsadaMember。

## instanceof
instanceof是java的運算子之一，用來測試一個實例（instance）是否屬於某個class或屬於該class的subclass。
```java
	AkukinMember a = new AkukinMember("湊あくあ", 1000);
	HololiveMember h = a;
		
	System.out.println(a instanceof AkukinMember);  //true
//	System.out.println(a instanceof UsadaMember);  //complie error
	System.out.println(a instanceof HololiveMember);  //true

	System.out.println(h instanceof AkukinMember);  //true
	System.out.println(h instanceof UsadaMember);  //false
	System.out.println(h instanceof HololiveMember);  //true
```
### instanceof範例
```java
package kensetsu;

public class Stream {
	
	public static void startStream(HololiveMember liver) {
		System.out.println("ホロ鯖をログインしました！");
		liver.buildHouse(2);
		if (liver instanceof AkukinMember) {
			((AkukinMember) liver).tara += 20;
			System.out.println("今のタラ：" + ((AkukinMember) liver).tara);
		}
		if (liver instanceof UsadaMember) {
			((UsadaMember) liver).ninjin += 30;
			System.out.println("今のにんじん：" + ((UsadaMember) liver).ninjin);
		}
	}

	public static void main(String[] args) {
		AkukinMember a = new AkukinMember("湊あくあ", 1000);
		UsadaMember u = new UsadaMember("Moona", 100);
		Stream.startStream(a);
		Stream.startStream(u);
	}

}

```
```
ホロ鯖をログインしました！
湊あくあ、家を作った<Akukin建設>
湊あくあ、家を作った<Akukin建設>
今のタラ：1020
ホロ鯖をログインしました！
Moona、家を作った<兎田建設>
Moona、家を作った<兎田建設>
今のにんじん：130
```

## 練習
Hololive成員都有一個姓名，且都會開實況（startStream），開實況都會說"こんにちは"。

Hololive成員有鯊魚、船長等角色（subclass），鯊魚再開實況時則是說"A"，船長則會說"Ahoy"。

並且，有一個Youtube的類別，有一個static的live的方法，其參數是Hololive成員，當live方法被呼叫時，會呼叫參數Hololive成員的startStream方法。

在Controller類別中有一個main方法，當main被呼叫時會宣告一隻鯊魚，叫"Gura"，一隻船長叫"マリン"，一個普通的Hololive成員叫"ときのそら"，並呼叫3次Youtube.live方法，參數分別是上述這3個角色。