###### tags: `JAVA`
# 01. Java Hello world

## 1. 基本變數型態

型態類型|	關鍵字|	位元數|	範圍
-|-|-|-
整數|	byte|	8|	-128 ～ 127
整數|	short|	16|	-32768 ～ 32767
整數|	int|	32|	-2147483648 ～ 2147483647
整數|	long|	64|	-9223372036854775808 ～ 9223372036854775807
浮點數|	float|	32|	依據 IEEE 754 標準
浮點數|	double|	64|	依據 IEEE 754 標準
布林值|	boolean|	1|	true, false
字元|	char|	16|	'\u0000' - '\uffff'

```java=
package helloWorld;

public class Main {

	public static void main(String[] args) {
		int a = 10;
		
		float f1 = 3.14f;
		float f2 = 3.14F;
		
		double d1 = 3.14;
		double d2 = 3l;
		double d3 = 3L;
		
		boolean b = true;
		
		char c1 = 'a';
		char c2 = '\n';
		char c3 = '我';
		
	}

}
```

## 2. Object

Object被所有的物件所繼承。

回傳型態|	Object的方法
-|-
Object|	clone()
boolean|	equals(Object obj)
void|	finalize()
Class\<?>|	getClass()
int|	hashCode()
void|	notify()
void|	notifyAll()
String|	toString()
void|	wait()
void|	wait(long timeout)
void|	wait(long timeout, int nanos)

```java=
package helloWorld;

public class Main {

	public static void main(String[] args) {
		Object a = new Object();
		System.out.println(a.toString());
	}

}
```
建立物件須使用關鍵字 **new** ，以及物件的建構子 (constructor) 。

建構子類似物件的方法 (method) ，用來專門建立物件之用。

一旦物件建立之後，物件就會包含許多屬性與方法。

### String

String (字串) 是一個常用又特別的物件。

建立String物件時，可以使用雙引號，不需使用new與constructor。

但若使用雙引號建立String，若內容相同則reference會相同。

使用==運算子可以判斷物件的reference是否相同。

使用equals方法可以判斷就算reference不同，但內容是否相同。

```java=
package helloWorld;

public class Main {

	public static void main(String[] args) {
		String a = "PekoPekoPeko";
		String b = "PekoPekoPeko";
		System.out.println(a == b); //true

		String a1 = new String("PekoPekoPeko");
		String b1 = new String("PekoPekoPeko");
		System.out.println(a1 == b1); //false
		System.out.println(a1.equals(b1)); //true
		
	}

}
```

## 3. System Output

* System.out.print
  * 輸出String, int, float, boolean...
* System.out.println
  * 輸出String, int, float, boolean...並換行
* System.out.printf
  * 如同C的printf

```java=
package helloWorld;

public class Main {

	public static void main(String[] args) {
		int a = 10;
		
		System.out.println("I have " + a + " apples.");
		System.out.printf("I have %d apples.\n", a);
		
	}

}
```
String可以藉由+來做字串串接，也可以+上其他類別或變數（該物件/變數會轉型成String）

## 4. java.util.Scanner 做 System Input
```java
import java.util.Scanner;
```
java.util的util是utility的意思，提供了許多類別，如集合 (ArrayList、HashMap等) 、隨機數產生、屬性檔案讀取、定時器等。

```java=
package helloWorld;
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		int a;
		double d;
		String s1;
		String s2;
		System.out.print("Input an int: ");
		a = scanner.nextInt();
		System.out.print("Input a double: ");
		d = scanner.nextDouble();
		System.out.print("Input a word: ");
		s1 = scanner.next();
		scanner.nextLine(); //去掉上一行留下的enter（換行）
		System.out.print("Input a sentence: ");
		s2 = scanner.nextLine();
		
		System.out.print(
				"int: " + a + "\n" + 
				"double: " + d + "\n" + 
				"word: " + s1 + "\n" + 
				"sentence: " + s2 + "\n");
		scanner.close();
	}

}
```
```
Input an int: 10
Input a double: 3.14159
Input a word: apple
Input a sentence: peko peko peko
int: 10
double: 3.14159
word: apple
sentence: peko peko peko

```