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

* String -&gt; int

```text
String s = "123";
int i1 = Integer.parseInt(s);
Integer i2 = Integer.valueOf(s);
```

