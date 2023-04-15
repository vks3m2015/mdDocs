
# _Diffrence between map() and flatMap() in Stream_

map() and flatMap() both are _intermediate operation_. Intermediate operations are invoked on a Stream instance and after processing, they return a Stream instance as output.

   ## map() ##
   
   When called on a stream it returns a new stream consisting of the results of applying the given function to the each element of the stream.
   
   **Method Syntax**
   
   ```sh
   <R> Stream<R> map(Function<? super T, ? extends R> mapper);
   ```
   * R is element type of new stream
   * mapper is a function to apply to each element of the stream
   
   **Example**
   
   Lets suppose we have list of integers and we have to multiply each element of the list with number 5
   
   ```java

   List<Integer> list = Arrays.asList(4, 7, 9, 13, 5);
   List<Integer> newList = list.stream()
                           .map( number -> number * 5)
						   .collect(Collectors.toList())
   
   ```
	  
   ## flatMap ##
   
   **Method Syntax**
   
   ```java
   <R> Stream<R> flatMap(Function<? super T, ? extends Stream<? extends R>> mapper);
   ```
   
   * R The element type of the new streamParameters
   * mapper is function to apply to each element which produces a stream of new values
   
   When called on a stream it returns a new stream consisting of the results of replacing each element of this stream with the contents of a mapped stream produced by applying the provided mapping function to each element.
   
   The flatMap() operation has the effect of applying a one-to-many transformation to the elements of the stream and then flattening the resulting elements into a new stream. 
   
   **Example**
   
   Lets suppose we have Stream of Orders and each order contains list of Items. Now if we want Stream of all the Items of all the Orders then we can use flatMap
  

```java
    // orders is List<Order> and each Order has List<Item> that is List of Item
	List<Item> items = orders.stream()
	                         .flatMap(order -> order.getItems().stream())
							 .collect(Collectors.toList())
```

   
   