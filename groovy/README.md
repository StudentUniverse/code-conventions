## Table of Contents

  1. [Semicolons Always](#semicolons-always)
  1. [Return Keyword](#return-keyword)
  1. [Def and type](#def-and-type)
  1. [Parentheses](#parentheses)
  1. [Getters and Setters](#getters-and-setters)
  1. [Initializing benas](#initializing-beans)
  1. [With](#with)

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

inspired by
http://groovy-lang.org/style-guide.html#_return_keyword_optional
