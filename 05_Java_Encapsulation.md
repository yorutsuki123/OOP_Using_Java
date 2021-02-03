###### tags: `JAVA`
# 05. 封裝（Encapsulation）

## 物件導向四個特性：
* 抽象（Abstraction）
* 封裝（Encapsulation）
* 繼承（Inheritance）
* 多型（Polymorphism）

## 封裝
> 在物件導向程式設計方法中，封裝（英語：Encapsulation）是指，一種將抽象性函式介面的實作細節部份包裝、隱藏起來的方法。同時，它也是一種防止外界呼叫端，去存取物件內部實作細節的手段，這個手段是由程式語言本身來提供的。封裝被視為是物件導向的四項原則之一。
> [name=wikipedia]

## 存取層級

關鍵字|	類別內部|	相同套件類別|	不同套件類別
-|-|-|-
public|可存取|	可存取|	可存取
protected|可存取|	可存取|	子類別可存取
（預設）|	可存取|	可存取|	不可存取
private|	可存取|	不可存取|	不可存取

對於一些attribute，我們可能不希望其他物件任意地去修改，這時我們可以把attribute設為private。
若要讓其他物件進行存取，可使用getter與setter來作為公共的存取介面。
```java
package hololive;

import java.util.Calendar;
import java.util.Date;

public class HololiveMember {
	
	private String name;
	private String nickname;
	private int generation;
	private static int memberCount = 0;
	
	public HololiveMember (String n, int g) {
		name = n;
		generation = g;
		nickname = "";
		memberCount++;
	}

	public HololiveMember (String n, String nn, int g) {
		name = n;
		generation = g;
		nickname = nn;
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
	
	public String getName() {
		return name;
	}

	public String getNickname() {
		return nickname;
	}
	
	public void setNickname(String n) {
		if (!name.equals(n))
			nickname = n;
	}
	
	public int getGeneration() {
		return generation;
	}
	
}
```
```java
package hololive;

public class Main {

	public static void main(String[] args) {
		HololiveMember member = new HololiveMember("白上フブキ", "FBK", 1);
		System.out.println(member.getName() + "\n-----");
		member.startStream();
	}

}
```