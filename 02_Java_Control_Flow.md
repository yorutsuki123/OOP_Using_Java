###### tags: `JAVA`
# 02. 流程控制

## 1. if else
跟C差不多，只是括號內只能是boolean

下面範例的method使用了foreach敘述句XD
```java
package controlFlow;

public class PasswordChecker {

	private static boolean hasUpper(String s) {
		for (char c: s.toCharArray()) {
			if (Character.isUpperCase(c))
				return true;
		}
		return false;
	}

	private static boolean hasLower(String s) {
		for (char c: s.toCharArray()) {
			if (Character.isLowerCase(c))
				return true;
		}
		return false;
	}

	private static boolean hasDigit(String s) {
		for (char c: s.toCharArray()) {
			if (Character.isDigit(c))
				return true;
		}
		return false;
	}
	
	public static void main(String[] args) {
		
		String password = "P@ssw0rd";
		
		if (password.length() < 8) {
			System.out.println("Too short");
		}
		else if (!hasUpper(password)) {
			System.out.println("Lack upper case");
		}
		else if (!hasLower(password)) {
			System.out.println("Lack lower case");
		}
		else if (!hasDigit(password)) {
			System.out.println("Lack digit");
		}
		else {
			System.out.println("Perfect");
		}

	}

}

```

## 2. switch case
跟C差不多，但可以處理String
```java
package controlFlow;

public class SwitchTest {

	public static void main(String[] args) {
		String a = new String("peko");
        
		switch (a) {
		case "PEKO":
			System.out.println("A");
			break;
		case "peko":
			System.out.println("B"); //B
			break;
		case "Peko":
			System.out.println("C");
			break;
		default:
			System.out.println("D");
		}
		
	}

}
```

## 3. while / do while
跟C差不多，只是括號內只能是boolean

## 4. for / foreach
for跟C差不多，只是判斷句只能是boolean。

foreach是C所沒有的語法，用途是走訪容器 (如array、List、Set等) 中的元素。
```java
package controlFlow;

public class ForTest {

	public static void main(String[] args) {
		String[] strs = {"あやめ", "すいちゃん", "フブキ"};
		
		for (int i = 0; i < strs.length; i++)
			System.out.println(strs[i]);
		
		for (String s: strs)
			System.out.println(s);
	}

}
```

