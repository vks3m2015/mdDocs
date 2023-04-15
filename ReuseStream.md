# Can we reuse stream?

**No**. We cann't reuse the stream. Stream throw IllegalStateException if it detects that the stream is being reused. 

```sh
IllegalStateException: stream has already been operated upon or closed.
```

We can invoke intermediate or terminal operation on a stream only once. 

```java
    List<Integer> list = Arrays.asList(3,2,5,1);
		
	//Creating stream
	Stream<Integer> stream = list.stream();
		
	//calling terminal operation on this stream
	Optional<Integer> first = stream.findFirst();
	System.out.println(" First element of list = "+ first.get());
			
	//calling terminal operation on the same stream AGAIN
	Optional<Integer> any = stream.findAny();
	System.out.println(" A member element of list = "+ any.get());
```

Output 

```sh
First element of list = 3
Exception in thread "main" java.lang.IllegalStateException: stream has already been operated upon or closed
	at java.base/java.util.stream.AbstractPipeline.evaluate(AbstractPipeline.java:229)
	at java.base/java.util.stream.ReferencePipeline.findAny(ReferencePipeline.java:652)
	at streams.ReusingStreams.exceptionReusing(ReusingStreams.java:66)
	at streams.ReusingStreams.main(ReusingStreams.java:15)

```

After calling operation findFirst() stream is closed. Now when calling findFirst() on the closed stream it will throw exception.

Similary calling intermediate operation twice on same stream will throw Exception
```java
    List<Integer> list = Arrays.asList(3,2,5,1);
		
	//Creating stream
	Stream<Integer> stream = list.stream();
		
	//calling intermediate operation on this stream
	Stream<Integer> gtTwoElements = stream.filter( e -> e > 2);
		
	//calling another intermediate operation on the same stream AGAIN. 
	//It will throw Exception at below line.
	Stream<Integer> multiplyTwo = stream.map( e -> e*2 );
```

So for this use case, we need to create fresh stream every time we want to use stream.

```sh
    List<Integer> list = Arrays.asList(3,2,5,1);
	Optional<Integer> first = list.stream().findFirst();
	Optional<Integer> any = list.stream().findAny();
```
Or We can also use a __Supplier__ to supply a new stream every time we want to use stream. Here is the way to do so-

```java
	List<Integer> list = Arrays.asList(3,2,5,1);
		
	//Supplier
	Supplier<Stream<Integer>> supplier = () -> list.stream();
	
	Optional<Integer> first = supplier.get().findFirst();
	System.out.println(" First element of list = "+ first.get());
			
	Optional<Integer> any = supplier.get().findAny();
	System.out.println(" A member element of list = "+ any.get());
```

