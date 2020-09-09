# Conversions

Java solutions to convert among types:

* char digit -&gt; int

```text
char c = '7';
int i = c - '0'; // i = 7
```

* ASCII code \(int\) -&gt; String

```text
int ascii = 65;
char c = (char) ascii;
String s = Character.toString(c);
```

* String -&gt; int/Integer

```text
String s = "123";
int i1 = Integer.parseInt(s);
Integer i2 = Integer.valueOf(s);
```

* int -&gt; String

```text
int i = 123;
String s1 = String.valueOf(i);
String s2 = Integer.toString(i);
```

