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
## Example 4
   ### Java8
```
    Stream.of("d2", "a2", "b1", "b3", "c")
    .map(s -> {
        return s.toUpperCase();
    })
    .filter(s -> {
        return s.startsWith("A");
    })
    .forEach(s -> System.out.println("forEach: " + s));
```
   ### Groovy
```
        List<String> values = ["d2", "a2", "b1", "b3", "c"]
        values.collect{it -> it.toUpperCase()} .findAll{it.contains("A")}.each {it -> println it}
    
```


  ### O/P
```
 A2
```

# Collect

Collect is an extremely useful terminal operation to transform the elements of the stream into a different kind of result, e.g. a List, Set or Map

### Most code samples from this section use the following list of persons for demonstration purposes:

```
class Person {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return name;
    }
}

List<Person> persons =
    Arrays.asList(
        new Person("Max", 18),
        new Person("Peter", 23),
        new Person("Pamela", 23),
        new Person("David", 12));
```

## Example 5

   ### Get the list of name starts with P
   
   ### Java8
```
    List<Person> filtered =
    persons
        .stream()
        .filter(p -> p.name.startsWith("P"))
        .collect(Collectors.toList());

     System.out.println(filtered);    // [Peter, Pamela]

```
   ### Groovy
```
       List filtered = persons.findAll{it -> it.name.startsWith('P')}
       println filtered    
    
```
   ### 
    [Peter, Pamela]


