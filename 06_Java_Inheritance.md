###### tags: `JAVA`
# 06. 繼承（Inheritance）
## 繼承
若一個子類別繼承一個父類別，則子類別可擁有父類別的屬性與方法，也可以根據需求，經由覆寫修改方法。

### extends
子類別可以使用extends來繼承父類別。

### super
子類別可以使用super來存取父類別。

相對於this是存取自己的屬性與方法。

### @Override
在方法前一行加上@Override來說明此方法覆寫了父類別的方法。

### 範例

```java
package hololive;

public class SetValueException extends Exception {

	public SetValueException() {
		super();
	}

	public SetValueException(String message) {
		super(message);
	}

}
```
```java
package hololive;

import java.util.Calendar;
import java.util.Date;

public class HololiveMember {
	
	private static int memberCount = 0;
	protected String name;
	protected String nickname;
	protected int generation;
	
	public HololiveMember (String n, int g) {
		name = n;
		generation = g;
		nickname = "";
		memberCount++;
	}
	
	public static void printMemberCount() {
		System.out.println("Member count: " + memberCount);
	}
	
	private void selfIntro() {
		System.out.printf("みなさん、こんにちは、私はホロライブ%d期生の%sです！\n",
				generation, name);
	}
	
	public void startStream() {
		Calendar c = Calendar.getInstance();
		Date d = c.getTime();
		System.out.printf("今は%tR、配信の時間だ！\nはい！\n", d);
		selfIntro();
	}
	
	public void buildHouse(int n) {
		for (int i = 0; i < n; i++) {
			System.out.println("家を作った");
		}
	}
	
	public String getNickname() {
		return nickname;
	}
	
	public void setNickname(String n) throws SetValueException {
		if (name.equals(n) || "".equals(n))
			throw new SetValueException();
		else
			nickname = n;
	}
	
	public String getName() {
		return name;
	}

	public int getGeneration() {
		return generation;
	}
	
}
```
```java
package hololive;

public class AkukinMember extends HololiveMember {
	
	private String position;
	private int tara;
	
	public AkukinMember(String n, int g, String p) {
		super(n, g); //Must be the first statement
		position = p;
		tara = 0;
	}

	public AkukinMember(String n, int g) {
		super(n, g);
		position = "員工";
		tara = 0;
	}
	
	@Override
	public void buildHouse(int n) {
		super.startStream();
		for (int i = 0; i < n; i++) {
			System.out.println(name + "、家を作った<Akukin建設>");
		}
	}
	
	public String getPosition() {
		return position;
	}
	
	public int getTara() {
		return tara;
	}
	
	public int modifyTara(int delta) throws SetValueException {
		if (tara + delta > 0)
			tara += delta;
		else
			throw new SetValueException();
		return tara;
	}
	
}
```
```java
package hololive;

public class Main {

	public static void main(String[] args) {
		
		AkukinMember m = new AkukinMember("ミオ", 2, "人事");
		m.buildHouse(3);
		try {
			m.modifyTara(30);
		}
		catch (SetValueException e) {
			System.out.println(e);
		}
		System.out.println(m.getName() + "が持っているテラ：" + m.getTara() + "個");
	}

}
```
### UML圖
![](https://i.imgur.com/jLtvS48.png)


## 轉型

### 向上轉型
以下這是合法的
```java
class A{

}

class B extends A{
	
	public static void main(String[] args) {
		A a = new B();
	}
	
}
```

### 向下轉型
以下是非法的
```java
class A{
	
}

class B extends A{
	
	public static void main(String[] args) {
		B b = (B)new A(); //ERROR
	}
	
}
```
以下這是合法的
```java
class A{
	
}

class B extends A{
	
	public static void main(String[] args) {
		A a = new B();
		B b = (B)a;
	}
	
}

```

## 多層繼承的初始化
```java
class A{
    A(){
        System.out.println("A constructor..");
    }
}
class B extends A{
    B(){
        System.out.println("B constructor..");
    }
}
class C extends B{
    C(){
        System.out.println("C constructor..");
    }
    
    public static void main(String[] args) {
        C c = new C();
    }
    
}
```
```
A constructor..
B constructor..
C constructor..
```