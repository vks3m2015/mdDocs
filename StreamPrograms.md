stream programs
-------------
**Find duplicate elements in a list**

```sh

List<Integer> list = Arrays.asList(2,10,2,5,15,10,2);
//Method - 1 


    Set<Integer> duplicates = list.stream()
				.filter(num -> Collections.frequency(list, num) > 1)
				.collect(Collectors.toSet());
		
		
//Method - 2 
	Set<Integer> set = new HashSet<>();
	Set<Integer> duplicates2 = list.stream()
				.filter(num -> !set.add(num))
				.collect(Collectors.toSet());

```



**Find average of odd integres of a list**

```sh
List<Integer> list = Arrays.asList(1,2,3,4,5);

		double avg = list.stream()
		               .filter(e -> e%2 == 1)
					   .mapToInt(e -> e.intValue())
					   .average()
					   .getAsDouble();

```


**Square the integres and find average of those squares values that are less than 100**

```sh

List<Integer> list = Arrays.asList(2,10,12,5,15);
		
		double avg = list.stream()
				.map(num -> num * num)
				.filter(squNum -> squNum < 100)
				.mapToInt(squNum -> squNum)
				.average()
				.getAsDouble();
		
		System.out.println(" avg = "+avg);


```





**Find sum of squares of ages of the Employees whose age is a Odd number**


Method -1 

```sh

List<Employee> list = //List of Employees

int sum = list.stream()
				.filter(emp -> emp.age % 2 != 0)
				.map( emp -> emp.age * emp.age)
				.mapToInt(age2 -> age2.intValue())
				.sum();
				
```

Method 2
```sh
int sum2 = list.stream()
				.filter(emp -> emp.age % 2 != 0)
				.map( emp -> emp.age * emp.age)
				.reduce( (a,b) -> a+b)
				.get();

```

***Find list of integers those starts with number 1 from list of integers***

```sh
 List<Integer> list = Arrays.asList(10, 15, 5, 20, 25, 100);
	
		List<Integer> list2 = list.stream()
				.filter(n -> String.valueOf(n).startsWith("1"))
				.collect(Collectors.toList());
		
		System.out.println(list2);

```

**Given list of Employees, find a map from the list having city as key and total number of employess in that city as value**

```sh


List<Employee> empList = Arrays.asList(
				new Employee(222, "A", 2000, "Knp", "UP"),
				new Employee(111, "B", 3000, "Knp", "UP"), 
				new Employee(333, "C", 3500, "Pune", "MH"),
				new Employee(123, "D", 3700, "Mumbai", "MH"));
				
				Map<String, Long> countEmployeeByState = empList.stream()
				.collect(Collectors.groupingBy(emp -> emp.state, Collectors.counting()));
		System.out.println("countEmployeeByState = "+countEmployeeByState);

``` 