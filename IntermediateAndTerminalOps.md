
# Intermediate and Terminal Operations in Java Stream

## Intermediate Operations

- When an intermediate operation is called on a stream, it returns another stream.
- Intermediate Operations are lazy. When we invoke an intermediate operation on a stream, the operation is not executed immediately. It is executed only when a terminal operation is invoked on that stream. Intermediate operations are memorized and are executed as soon as a terminal operation is invoked.

Some Intermediate operations are - 
```
map(), filter(), distinct(), sorted(), limit(), skip()
```

## Terminal Operations

- Terminal operations produce result after all the intermediate are applied on the stream. 

Some Intermediate operations are - 
```
forEach(), toArray(), reduce(), collect(), min(), max(), count(), 
anyMatch(), allMatch(), noneMatch(), findFirst(), findAny()  
```