
## Java Concepts Through Programs

**1**. Will is compile successfully? 

```sh
public class ExceptionQues {

	public static void main(String[] args) {
		ExceptionQues obj = new ExceptionQues();
		obj.m();
	}
	
	public void m() {
		throw new RuntimeException(new Exception("This is an Exception"));
	}
}


```