###### tags: `JAVA`
# 04. Class

## 1. Class vs Object

![](https://i.imgur.com/khiDPMe.png)
圖片素材取自https://www.hololive.tv/member

## 2. Attribute

class的attribute，可分為public、private、protected等權限的屬性

```java
package hololive;

class Date {
	
	public int month;
	public int day;
	
}

public class HololiveMember {
	
	public String name;
	public String youtubeID;
	public Date birthDay;
	public double height;
	public double weight;
	
}
```
### attribute存取權限

attribute關鍵字|	類別內部|	相同套件類別|	不同套件類別
-|-|-|-
public|可存取|	可存取|	可存取
protected|可存取|	可存取|	子類別可存取
無|	可存取|	可存取|	不可存取
private|	可存取|	不可存取|	不可存取

### class存取權限

class關鍵字|相同套件類別|	不同套件類別
-|-|-|-
public|可存取|	可存取
無|可存取|	不可存取

## 3. Constructor

當建立一個object時，所使用的new後面接的像是function的東西叫做constructor。

若class沒有定義constructor，該class會預設一個空的，但若class有定義constructor，則無法再使用預設的。

```java
package hololive;

class Date {
	
	public int month;
	public int day;
	
}

public class Main {

	public static void main(String[] args) {
		Date date = new Date(); //預設的constructor
		date.month = 10;
		date.day = 5;
	}

}

```
定義constructor
```java
package hololive;

class Date {
	
	public int month;
	public int day;
	
	public Date (int m, int d) { //Define constructor
		this.month = m;
		this.day = d;
	}
	
}

public class Main {

	public static void main(String[] args) {
		Date date = new Date(10, 5);
//		Date date = new Date(); //ERROR, Date() is undefined
	}

}
```
可以定義多個constructor
```java
package hololive;

class Date {
	
	public int month;
	public int day;
	
	public Date () {
	}
	
	public Date (int m, int d) {
		month = m;
		day = d;
	}
	
	public Date (String s, String split) {
		String[] a = s.split(split);
		month = Integer.parseInt(a[0]);
		day = Integer.parseInt(a[1]);
	}
	
}

public class Main {

	public static void main(String[] args) {
		Date date1 = new Date();
		Date date2 = new Date(10, 5);
		Date date3 = new Date("12/13", "/");
		System.out.println(date2.month + "/" + date2.day); // 10/5
		System.out.println(date3.month + "/" + date3.day); // 12/13
	}

}
```

### this

在class中的constructor或method中，`this`代表自己這個object，例如`this.month`就是自己的month屬性。

但是如果在該constructor或method中，若要存取自己的attribute，且沒有其他變數名稱與要存取的自己的attribute同名，則可以省略`this.`。

## 4. Method

如果說attribute是一個物件所擁有的東西，那麼method就是一個物件所能做的動作。

```java
package hololive;

class Date {
	
	public int month;
	public int day;
	
	public Date () {
	}
	
	public Date (int m, int d) {
		month = m;
		day = d;
	}
	
	public Date (String s, String split) {
		String[] a = s.split(split);
		month = Integer.parseInt(a[0]);
		day = Integer.parseInt(a[1]);
	}
	
}

public class HololiveMember {
	
	public String name;
	public int generation;
	public String youtubeID;
	public Date birthDay;
	public double height;
	public double weight;
	
	public HololiveMember (String n, int g, String yid, Date bd, double h, double w) {
		name = n;
		generation = g;
		youtubeID = yid;
		birthDay = bd;
		height = h;
		weight = w;
	}
	

	public HololiveMember (String n, int g, String yid, Date bd) {
		name = n;
		generation = g;
		youtubeID = yid;
		birthDay = bd;
	}
	
	public void selfIntro () {
		System.out.printf("みなさん、こんにちは、私はホロライブ%d期生の%sです！\n",
				generation, name);
	}
	
}
```

```java
package hololive;

public class Main {

	public static void main(String[] args) {
		HololiveMember member = new HololiveMember(
				"湊あくあ", 3, "UC1opHUrw8rvnsadT-iGp7Cg",
				 new Date(12, 1), 148, 44.5);
		
		member.selfIntro(); //みなさん、こんにちは、私はホロライブ3期生の湊あくあです！
	}

}
```

### 多載 Overload
多載（Overload）指在一個類別（class）中，定義多個名稱相同，但參數不同的method。

例如剛剛我們定義了多個constructor，被稱為constructor overloading，而理所當然，method也可以overloading。

```java
public class HololiveMember {
	
	public String name;
	public int generation;
	public String youtubeID;
	public Date birthDay;
	public double height;
	public double weight;
	
	public HololiveMember (String n, int g, String yid, Date bd, double h, double w) {
		name = n;
		generation = g;
		youtubeID = yid;
		birthDay = bd;
		height = h;
		weight = w;
	}
	

	public HololiveMember (String n, int g, String yid, Date bd) {
		name = n;
		generation = g;
		youtubeID = yid;
		birthDay = bd;
	}
	
	public void selfIntro () {
		System.out.printf("みなさん、こんにちは、私はホロライブ%d期生の%sです！\n",
				generation, name);
	}
	
	public void superChat (double money) {
		System.out.printf("スパチャありがとうね！\n");
	}
	
	public void superChat (double money, String text) {
		System.out.printf("スパチャ、”%s”、ありがとう！\n", text);
	}
	
}
```