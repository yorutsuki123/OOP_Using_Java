###### tags: `JAVA`
# 03. Array 與 String

## 1. 一維陣列

宣告陣列變數並指派陣列
```java
package arrayAndString;

public class ArrayDecl {

	public static void main(String[] args) {
		//Empty array
		int[] iArr = new int[5];
		double[] dArr = new double[5];
		char[] cArr = new char[5];
		
		iArr[0] = 10;
		iArr[1] = 20;
		iArr[2] = 30;
		
		for (int i: iArr) //10 20 30 0 0
			System.out.print(i + " ");
		
		//let iArr become a new empty array
		iArr = new int[10];

	}

}
```
宣告陣列變數並指派指定數值的陣列
```java
package arrayAndString;

public class ArrayDecl {

	public static void main(String[] args) {
		//declare array when declaring variable
		int[] iArr1 = new int[]{10, 20, 30};
		double[] dArr1 = new double[]{10.0, 20.0, 30.0};
		char[] cArr1 = new char[]{'a', 'b', 'c'};
		
		//or usually
		int[] iArr2 = {10, 20, 30};
		double[] dArr2 = {10.0, 20.0, 30.0};
		char[] cArr2 = {'a', 'b', 'c'};
		
		//print iArr1
		for (int i: iArr1) //10 20 30 
			System.out.print(i + " ");
		System.out.println();
		
		//declare array after declaring variable
		iArr1 = new int[]{12, 25};
		
		for (int i: iArr1) //12 25
			System.out.print(i + " ");
		System.out.println();

	}

}
```
以下是錯誤的
```java
package arrayAndString;

public class ArrayDecl {

	public static void main(String[] args) {
		int[] iArr1 = new int[3]{10, 20, 30}; //ERROR
		iArr1 = {12, 25}; //ERROR
		iArr1 = new int[2]{12, 25}; //ERROR
	}

}
```

### 取得陣列長度

取得屬性`length`

```java
package arrayAndString;

public class ArrayLen {

	public static void main(String[] args) {
		int[] iArr = {10, 20, 30};
		System.out.println(iArr.length); //3
	}

}
```

## 2. 多維陣列

未指定值（預設0）

```java
package arrayAndString;

public class MultiDegreeArrayDecl {

	public static void main(String[] args) {
		//對稱 Rectangular
		int[][] iArr1 = new int[2][3];
        
		//非對稱 Non-Rectangular
		int[][] iArr2 = new int[2][];
		iArr2[0] = new int[3];
		iArr2[1] = new int[4];
	}

}
```
有指定初始值
```java
package arrayAndString;

public class MultiDegreeArrayDecl {

	public static void main(String[] args) {
		//對稱 Rectangular
		int[][] iArr1 = {{2, 3, 4}, {3, 4, 5}};
		for (int[] a: iArr1) {
			for (int i: a) {
				System.out.print(i + " ");
			}
			System.out.println();
		}
		//非對稱 Non-Rectangular
		int[][] iArr2 = {{2, 3, 4}, {3, 4}};
		for (int[] a: iArr2) {
			for (int i: a) {
				System.out.print(i + " ");
			}
			System.out.println();
		}
		
	}

}
```

## 3. Object Array

不只要new Object Array，Array的元素也都要new。
```java
package arrayAndString;

public class ObjectArrayTest {

	public static void main(String[] args) {
		Object[] a = new Object[3];
		a[0] = new Object();
		a[1] = new Object();
		a[2] = new Object();
		
		Object[] b = {new Object(), new Object(), new Object()};
	}

}
```

Object Array比較親民的例子是String Array：
```java
package arrayAndString;

public class StrArrayTest {

	public static void main(String[] args) {
		String[] sArr = new String[3];
		sArr[0] = new String("Peko");
		sArr[1] = new String("Miko");
		sArr[2] = new String("Daisensou");
	}

}
```
也可以寫成
```java
package arrayAndString;

public class StrArrayTest {

	public static void main(String[] args) {
		String[] sArr = {
				new String("Peko"), 
				new String("Miko"), 
				new String("Daisensou")};
	}

}
```
但又因為是String，可以只使用雙引號而不用寫new和constructor
```java
package arrayAndString;

public class StrArrayTest {

	public static void main(String[] args) {
		String[] sArr = {"Peko", "Miko", "Daisensou"};
		
	}

}
```

## 4. java.util.Arrays的常用method

```java
package arrayAndString;

import java.util.Arrays;

public class ArraysTest {

	public static void main(String[] args) {
		int[] a = {30, 10, 20};
		int[] b = {30, 10, 20};
		int[] c = {30, 10, 40};
		//轉型為String
		System.out.println(Arrays.toString(a)); //[30, 10, 20]
		//搜尋
		System.out.println(Arrays.binarySearch(a, 20)); //2
		//比較
		System.out.println(Arrays.compare(a, b)); //0
		System.out.println(Arrays.compare(a, c)); //-1
		//內容是否相等
		System.out.println(Arrays.equals(a, b)); //true
		//排序
		Arrays.sort(a);
		System.out.println(Arrays.toString(a)); //[10, 20, 30]
		//填入
		Arrays.fill(a, -1);
		System.out.println(Arrays.toString(a)); //[-1, -1, -1]
	}

}
```

## 5. String常用的method
```java
package arrayAndString;

import java.util.Arrays;

public class StringMethodTest {

	public static void main(String[] args) {
		String s = "  Peko Miko Daisensou  ";
		System.out.printf("\"%s\"\n", s); //"  Peko Miko Daisensou  "
		//去除多餘空白
		String s2 = s.trim();
		System.out.printf("\"%s\"\n", s); //"  Peko Miko Daisensou  "
		System.out.printf("\"%s\"\n", s2); //"Peko Miko Daisensou"
		//字元取代
		String s3 = s.replace('o', '0');
		System.out.printf("\"%s\"\n", s); //"  Peko Miko Daisensou  "
		System.out.printf("\"%s\"\n", s3); //"  Pek0 Mik0 Daisens0u  "
		//字串取代
		String s4 = s.replaceAll("ko", "こ");
		System.out.printf("\"%s\"\n", s); //"  Peko Miko Daisensou  "
		System.out.printf("\"%s\"\n", s4); //"  Peこ Miこ Daisensou  "
		//字串切割
		String[] sArr = s2.split(" ");
		System.out.printf("\"%s\"\n", s2); //"Peko Miko Daisensou"
		System.out.printf("%s\n", Arrays.toString(sArr)); 
			//[Peko, Miko, Daisensou]
		//字串拼接
		String s5 = String.join("__", sArr);
		System.out.printf("\"%s\"\n", s5); //"Peko__Miko__Daisensou"
		//轉換為字元陣列
		char[] cArr = s2.toCharArray();
		System.out.printf("\"%s\"\n", s2); //"Peko Miko Daisensou"
		System.out.printf("%s\n", Arrays.toString(cArr)); 
			//[P, e, k, o,  , M, i, k, o,  , D, a, i, s, e, n, s, o, u]
		//轉換為全大寫
		String s6 = s3.toUpperCase();
		System.out.printf("\"%s\"\n", s3); //"  Pek0 Mik0 Daisens0u  "
		System.out.printf("\"%s\"\n", s6); //"  PEK0 MIK0 DAISENS0U  "
		//轉換為全小寫
		String s7 = s3.toLowerCase();
		System.out.printf("\"%s\"\n", s3); //"  Pek0 Mik0 Daisens0u  "
		System.out.printf("\"%s\"\n", s7); //"  pek0 mik0 daisens0u  "
		//判斷是否包含
		System.out.println(s.contains("Miko")); //true
		//尋找位置
		System.out.println(s.indexOf("Miko")); //7
	}

}
```