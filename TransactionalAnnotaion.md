
## Spring @Transactional Annotation


- We can declare @Transactional annotaion on a class or on an individual method.
- When this annotation is declared at the class level, it applies as a default to all methods of the declaring class and its subclasses.
- We should apply the @Transactional annotation only to methods with public visibility. If you do annotate protected, private, or package-visible       methods with the @Transactional annotation, no error is raised, but configured transactional settings will not apply on that method.



## @Transactional Settings

@Transactional annotaion is metadata. We can provide different transactional properties or settings while annotating this annotaion.
The default @Transactional settings are - 

- *Default Settings*
-  propagation -> PROPAGATION_REQUIRED
-  isolation -> ISOLATION_DEFAULT
-  readOnly -> false 
-  rollbackFor -> By default, a transaction will be rolling back on *RuntimeException* and *Error* but not on checked exceptions 

- **rollbackFor** -> 
   Defines zero (0) or more exception types, which must be subclasses of Throwable, indicating which exception types must cause a transaction rollback.
   By default, a transaction will be rolled back on RuntimeException and Error but not on checked exceptions (business exceptions).   

 