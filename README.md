# stream-api-java8-vs-groovy
  ##  Goovy alternative of Java8's stream operation

| Example   |     Java 8     |  Groovy |
|----------|:-------------:|------:|
| 1 | .filter & .map | findAll |
| 2 | .findFirst   |   take |
| 3 | .map |    .collect |
| 4 | .filter & .map | findAll |
| 5 | .filter & .collect  |   findAll |
| 6 | .groupingBy | .groupBy |
| 7 | .Collectors.toMap   |   .collectEntries |
| 8 | .reduce |    .inject |

## Example 1
   ### Java8
```
       List<String> myList =
                Arrays.asList("a1", "a2", "b1", "c2", "c1");
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


# Group By


## Example 6

   ### Group By Age
   
   ### Java8
```
   Map<Integer, List<Person>> personsByAge = persons
    .stream()
    .collect(Collectors.groupingBy(p -> p.age));

   personsByAge
    .forEach((age, p) -> System.out.format("age %s: %s\n", age, p));


```
   ### Groovy
```
      persons.groupBy {it -> it.age}.each { k,v -> println k + '' +  v}
    
```
   ### 
   
    18 [Max]
    23 [Peter, Pamela]
    12 [David]

## Example 7

   ### Converting toMap 
   
   ### Java8
```
   Map<Integer, String> map = persons
    .stream()
    .collect(Collectors.toMap(
        p -> p.age,
        p -> p.name,
        (name1, name2) -> name1 + ";" + name2));


```
   ### Groovy
```      
     Map filteredPerson = persons.groupBy {it -> it.age}.collectEntries { k,v -> [(k):v.join(';')]}
     println filteredPerson
```
   ### O/P 
   
// {18=Max, 23=Peter;Pamela, 12=David}

## Example 8

   ### Converting toMap 
   
   ### Java8
```
  persons
    .stream()
    .reduce((p1, p2) -> p1.age > p2.age ? p1 : p2)
    .ifPresent(System.out::println);    // Pamela

```
   ### Groovy
```      
        Person person = persons.inject { result1,result2 ->
            result1 = result1.age > result2.age ? result1 : result2
        }
        
        println person.name
```
   ### O/P 
   
// Pamela

