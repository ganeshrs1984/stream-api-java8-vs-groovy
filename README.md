# stream-api-java8-vs-groovy
Stream api java 8 - how to write the same in groovy

## Example 1
   ### Java8
```
myList
    .stream()
    .filter(s -> s.startsWith("c"))
    .map(String::toUpperCase)
    .sorted()
    .forEach(System.out::println);
```
   ### Groovy
``` 
        List<String> myList =
                Arrays.asList("a1", "a2", "b1", "c2", "c1");

        myList.findAll{it -> it.startsWith("c")}?.toSorted()?.each{it -> println it.toUpperCase()}
    
```

  ### O/P
```
  C1
  C2
```
## Example 2
   ### Java8
```
Arrays.asList("a1", "a2", "a3")
    .stream()
    .findFirst()
    .ifPresent(System.out::println);  // a1
```
   ### Groovy
```
   Arrays.asList("a1", "a2", "a3").take(1).each{it.println it}
    
```


  ### O/P
```
 a1
```

## Example 3
   ### Java8
```
Arrays.stream(new int[] {1, 2, 3})
    .map(n -> 2 * n + 1)
    .average()
    .ifPresent(System.out::println);  
```
   ### Groovy
```
        List<Integer> values = [1,2,3]
        println values.collect{it -> 2*it + 1}.sum()/ values.size()
    
```


  ### O/P
```
 5
```
