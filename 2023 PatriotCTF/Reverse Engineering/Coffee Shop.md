## Coffee Shop 


### Problem
```
I hate it when coffee shops misspell my name! Are you able to find what it is?

Flag format: CACI{FirstnameLastname}

Author: CACI
```
Files provided:
- CoffeeShop.jar
### Solution

A .jar file is given, which means that that [JD-GUI](http://java-decompiler.github.io/)should be the tool of choice. 

After decompiling CoffeeShop.jar, we are shown the following:
```java
import java.util.Base64;  
import java.util.Scanner;  
  
class CoffeeShop {  
  public static void failure() {  
    System.out.println("Sorry! You didn't get it right...");  
  }  
    
  public static void success() {  
    System.out.println("Nice! You got it!");  
    System.out.println("Submit the name you entered inside CACI{} to get points!");  
  }  
    
  public static void main(String[] paramArrayOfString) {  
    Scanner scanner = new Scanner(System.in);  
    System.out.println("What's my name?");  
    String str1 = scanner.nextLine();  
    String str2 = Base64.getEncoder().encodeToString(str1.getBytes());  
    if (str2.length() != 20) {  
      failure();  
    } else if (!str2.endsWith("NoZXI=")) {  
      failure();  
    } else if (!str2.startsWith("R2FsZU")) {  
      failure();  
    } else if (!str2.substring(6, 14).equals("JvZXR0aW")) {  
      failure();  
    } else {  
      success();  
    }   
  }  
}
```

There are 3 conspicuous strings: **"NoZXI="**, **"R2FsZU"**, **"JvZXR0aW"**

They are also put into methods that indicate where they should be placed relative to each other in order to make the flag.

Putting them in the correct order yields: **"R2FsZUJvZXR0aWNoZXI="**

This still doesn't look like a flag, but the import statements at the top of the file tell us that the string needs to be decoded from base64.

Any base64 decoder will work, but i use [base64decode.org](https://www.base64decode.org/).

**"R2FsZUJvZXR0aWNoZXI="** decodes to **"GaleBoetticher"**

All that needs to be done is wrap it in CACI{} like the beginning of the program tells us too.

Flag = `CACI{GaleBoetticher}`