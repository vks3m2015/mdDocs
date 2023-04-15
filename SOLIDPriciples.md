# SOLID Priciples

- S - Single Responsibility Priciple
- O - Open-Close Priciple
- L - Liskov Substitution Principle
- I - Interface Segregation Priciple
- D - Dependency Inversion Priciple

## Single Responsibility Priciple

SRP states that a class should only have __one responsibility__ therefore it should only have __one reason to change__.   

Let's we have a class ReportService 

```java

public class ReportService {

    public void buildReport() {
        //logic to build the Report
    }

	public void printReport() {
        //logic to print the Report
    }
	
	public void saveReportToFile() {
        //logic to save the Report in a file
    }
}
```

Here we can notice that ReportService class can be changed for two reasons. 
First, If there is any change in report building logic.
Second, If there is any change in printing report logic(ie - format of report to print is changed).
Third, If there is change in saving report

It would be a bad design to couple things that change for different reasons at different times.
Since these are different responsibilities, these methods should be kept in different classes. 

```java
public class BuildReportService{
    public void buildReport() {
        //logic to build the Report
    }
} 

public class PrintReportService {
    public void printReport() {
        //logic to print the Report on console
    }
}

pubic class ReportPersistance {
    public void saveReportToFile() {
        //logic to save the Report in a file
    }
}
```
The idea is to keep a class focused on a single responsibility.


## Open-Close Priciple

OCP states that software entities such as modules, classes, functions, etc. should be __open for extension, but closed for modification__.

So our design should be such that if there some new requirement comes up to add some new functionality to our code, we should be able to avoid modification of existing code. Because by modifying already tested code we are taking risk of creating new bugs.

We can add new functionalty to our code with the help of interfaces and abstract classes.

Now suppose in above example we have to save report in Database alse apart from saving in file. So our design for persisting Report should be as - 

```java

interface ReportPersistance {
  public void saveReport();
}


public class FilePersistance implements ReportPersistance  {
    @Override
	public void saveReport() {
      //logic to save the Report in a file
    }
}

public class DBPersistance implements ReportPersistance  {
    @Override
	public void saveReport() {
      //logic to save the Report in a Database
    }
}

```

## Liskov Substitution Principle

This principle states that subclasses should be substitutable for their base classes. 

If S is a subtype of T, then objects of type T in a program may be replaced with objects of type S without altering any of the desirable properties of that program.



## Interface Segregation Priciple

ISP states that clients should not be forced to implement a function they don't use or they don't need.
ISP splits interfaces that are very large into smaller and more specific ones so that clients will only have to know about the methods that are of interest to them.


## Dependency Inversion Principle
The Dependency Inversion principle states that our classes should depend upon interfaces or abstract classes instead of concrete classes and functions.  

