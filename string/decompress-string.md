---
description: String
---

# Decompress String

### Version 0

Given a string in compressed form, decompress it to the original string. The adjacent repeated characters in the original string are compressed to have the character followed by the number of repeated occurrences. If the character does not have any adjacent repeated occurrences, it is not compressed.

**Assumptions**

* The string is not null
* The characters used in the original string are guaranteed to be ‘a’ - ‘z’
* There are no adjacent repeated characters with length &gt; 9

**Examples**

* “acb2c4” → “acbbcccc”

```text
public String decompress(String input) {
    if (input.length() == 0) {
      return input;
    }

    StringBuilder sb = new StringBuilder();
    int count = 0;
    char tmpChar = input.charAt(0);
    for (char c: input.toCharArray()) {
      if (Character.isDigit(c)) {
        count = Character.getNumericValue(c);
        for (int i = 0; i < count - 1; i++) {
          sb.append(tmpChar);
        }
      } else {
        tmpChar = c;
        sb.append(tmpChar);
      }
    }

    return sb.toString();
}
```

