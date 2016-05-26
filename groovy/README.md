## Table of Contents

  1. [Semicolons Always](#semicolons-always)
  1. [Return Keyword](#return-keyword)
  1. [Def and type](#def-and-type)
  1. [Parentheses](#parentheses)
  1. [Getters and Setters](#getters-and-setters)
  1. [Initializing benas](#initializing-beans)
  1. [With](#with)
  1. [Strings](#strings)
  1. [Package Reference](#package-reference)
  1. [Conditionals](#conditionals)
  1. [Elvis](#elvis)

The [groovy language documentation](http://docs.groovy-lang.org/latest/html/documentation/index.htm) is a great place to learn
about all the different features the language offers. However, not every feature should be used because it could have
performance or maintenance draebacks and hence this document.
  

## Semicolons Always
Unlike Java semicolons do not cause compilation errors and are not required. However, to be consistent with our Java and
JavaScript standards always use semicolons.
```
//bad
println('bla')
//good
prinln('bla');
```
**[⬆ back to top](#table-of-contents)**

## Return Keyword
In Groovy, the last expression evaluated in the body of a method can be returned without necessitating the return keyword.
Always be explicit.
```
//bad
String toString() { "su strong" }
//good
String toString() { return "su strong" }
```

**[⬆ back to top](#table-of-contents)**

## Def and Type
Groovy does not require specifying types, but we do.
```
//bad
def name = "Jack""
//good
String name = "Jack"
```

**[⬆ back to top](#table-of-contents)**

## Parentheses
To be agreed upon

**[⬆ back to top](#table-of-contents)**

## Getters and Setters
Use shortcut setters and getters for properties.
```
class Person {
  String name;
}
Person pete = new Person(name: 'Pete');
//bad
pete.setName('John');
//good
pete.name = 'Rick';
```

**[⬆ back to top](#table-of-contents)**

## Initializing Beans
```
class Server {
    String name
    Cluster cluster
}

//bad
Server s = new Server();
s.name = 'Lizz';
s.cluster = someCluster;
//good
Sever s = new Server(name: 'Lizz', cluster: someCluster);
```

**[⬆ back to top](#table-of-contents)**

## With 

Named-parameters with the default constructor is interesting when creating new instances, but what if you are updating an instance that was given to you, do you have to repeat the 'server' prefix again and again? No, thanks to the with() method that Groovy adds on all objects of any kind:
```
server.name = application.name
server.status = status
server.sessionCount = 3
server.start()
server.stop()
vs:

server.with {
    name = application.name
    status = status
    sessionCount = 3
    start()
    stop()
}
```

**[⬆ back to top](#table-of-contents)**

## Strings
If no interpolation is required use [single quote strings](http://docs.groovy-lang.org/latest/html/documentation/index.html#_single_quoted_string).
```
String stringWithSingleQuote = 'an escaped single quote: \' needs a backslash';
String stringWithBackSlash = 'an escaped escape character: \\ needs a double backslash';
```

If interpolation is desired use [double quote strings](http://docs.groovy-lang.org/latest/html/documentation/index.html#_double_quoted_string).
```
//bad
println("Name is " + fName + " " + lName);
//good
println("Name is ${fName} ${lName}");
```

For multiline strings use `\` or """.
```
String multi1 = "line 1\
  line 2\
  line 3";
  
String muli2 = """line1
  line 2
  line 3""";
```

**[⬆ back to top](#table-of-contents)**

## Package Reference
Alway import packages instead of using inline package name.
This will help flag errors at compile time vs run time.
```
//bad
com.su.util.TimeHelper timeHelper = new com.su.util.TimeHelper();

//good
import com.su.util.TimeHelper
...
TimeHelper timeHelper = new TimeHelper();
```

If there are name conflicts use an import alias.
```
import com.su.util.TimeHelper as SuTimeHelper
import com.example.util.TimeHelper as ExampleTimeHelper
```

**[⬆ back to top](#table-of-contents)**

## Conditionals

Conditionals expect a boolean. Don't complicate by comparing booleans to a boolean, it runs the risk of using '=' instead of '=='.

```
///bad
if(someBool === true){
//easy to miss dangerous assignment if(someBool = true){

///good
if(someBool){
```

Always use brakets with conditionals.
```
//bad
if(bla) println('something');
//good
if(bad){
  println('something');
}
```

**[⬆ back to top](#table-of-contents)**

## Elvis
Elvis operator can be useful. If anything evaluates to null the following operation will not be executed.
```
//bad
if (order != null) {
    if (order.getCustomer() != null) {
        if (order.getCustomer().getAddress() != null) {
            System.out.println(order.getCustomer().getAddress());
        }
    }
}
//good
println order?.customer?.address
```

Can also be used for assignment.
```
//bad
String result = result != null ? result : 'default';
//good
String result = result ?: 'default';
```

**[⬆ back to top](#table-of-contents)**

Inspired by
http://groovy-lang.org/style-guide.html#_return_keyword_optional
