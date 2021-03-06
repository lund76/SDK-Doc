---
title: JSONBuilder
path: /EJScript/Classes/JSONBuilder
intellisense: 1
classref: 1
sortOrder: 442
---


The JSONBuilder class simplifies building JSON hierarchies. The result will be a string in correct JSON format, with string values properly escaped. This class is useful e.g. in combination with the HTTP class to make REST-calls.




###Example code:###


    JSONBuilder jb;
    jb.pushObject("");
    jb.pushArray("persons");
    
    jb.pushObject("");
    jb.addString("firstname", "John");
    jb.addInteger("age", 40);
    jb.popLevel();
    
    jb.pushObject("");
    jb.addString("firstname", "Peter");
    jb.addInteger("age", 34);
    jb.popLevel();
    
    jb.popLevel();
    jb.popLevel(); // jb.finalize() could be used to pop all levels
    print(jb.getString());




1. autolist

