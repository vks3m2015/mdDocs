Serialization
--------------------
Serialization is the conversion of the state of an object into a byte stream. These byte streams then can be saved to a database or transfer over a network.
Deserialization is the process of converting the serialized form of an object back into a copy of the object.

A Java object is serializable if its class or any of its superclasses implements either the java.io.Serializable interface or its subinterface, java.io.Externalizable. When a class implements the java.io.Serializable interface, all its sub-classes are serializable as well. 

The Serializable interface is a marker interface with no methods or fields. It works like a flag for the JVM.

When an object has a reference to another object, these objects must implement the Serializable interface separately, or else a NotSerializableException will be thrown

Serializing a object
------------------------

The Java serialization process provided by ObjectInputStream and ObjectOutputStream classes.
It has two methods -
```sh
public final void writeObject(Object o) throws IOException;
```
This method takes a serializable object and converts it into a sequence (stream) of bytes.
and
```sh
public final Object readObject() throws IOException, ClassNotFoundException;
```
This method can read a stream of bytes and convert it back into a Java object.


Lets serialize Person object. 

Note that 
* **static** fields belongs to class. Hence they are not serialized.
* we can use **transient** keyword to ignore a field from serialization




```sh
class Person implements Serializable{
	private static final long serialVersionUID = 1L;
	
	public int id;
	public String name;
	public transient String nickName;
	static String organisation = "XYZ";
	
	//Constructor
	//getter 
	//setter

}
```



```sh
 public class Serialization {

	public static void main(String[] args) throws IOException, ClassNotFoundException {
		
		Person person = new Person(123, "vks", "vikku", new Address("Knp", "India"));
		
		FileOutputStream fos = new FileOutputStream("Files/SerializationObject");
		ObjectOutputStream oos = new ObjectOutputStream(fos);
		oos.writeObject(person);
		oos.close();	
		
		FileInputStream fis = new FileInputStream("Files/SerializationObject");
		ObjectInputStream ois = new ObjectInputStream(fis);
		Person p = (Person)ois.readObject();
		ois.close();
		
		System.out.println(" Person = "+p);
		/*
		 * System.out.println("id  = "+ p.id); System.out.println("nick Nmae  = "+
		 * p.nickName); System.out.println("Organisation Name  = "+ p.organisation);
		 * System.out.println("Address   = "+ p.address);
		 */
	}
}
```


Lets assume there is a attribute in Person class Address that is not serializable. So we need to mark address member variable as transient otherwise a NotSerializableException will be thrown. We can still store address information of a Person using custom serialization. 
We can override default way of serialization of Java by providing two methods in the class that we want to serialize.

```sh
private void writeObject(ObjectOutputStream out) throws IOException;
```
and 

```sh
private void readObject(ObjectInputStream in) throws IOException, ClassNotFoundException;
```


```sh

class Person implements Serializable{
	private static final long serialVersionUID = 1L;
	
	public int id;
	public String name;
	public transient String nickName;
	static String organisation = "XYZ";
	public transient Address address; 
	
	//Constructor

	private void writeObject(ObjectOutputStream oos) throws IOException {
		oos.defaultWriteObject();
		oos.writeObject(address.city);
		oos.writeObject(address.country);
	}

	private void readObject(ObjectInputStream ois) throws ClassNotFoundException, IOException {
		ois.defaultReadObject();
		String city = (String) ois.readObject();
		String country = (String) ois.readObject();
		Address a = new Address(city, country);
		this.address = a;
	}
	
	//getter
	//setter

}

```


There are two other important methods are -


The writeReplace Method
----------------------------------------
For Serializable and Externalizable classes, the writeReplace method allows a class of an object to provide a replacement in the stream before the object is written.
The method is defined as follows:

```sh
   ANY-ACCESS-MODIFIER Object writeReplace() throws ObjectStreamException;
 ```  
The writeReplace method is called when ObjectOutputStream is preparing to write the object to the stream. The ObjectOutputStream checks whether the class defines the writeReplace method. If the method is defined, the writeReplace method is called to allow the object to designate its replacement in the stream. The object returned should be either of the same type as the object passed in or an object that when read and resolved will result in an object of a type that is compatible with all references to the object. If it is not, a ClassCastException will occur when the type mismatch is discovered.


The readResolve Method
-----------------------------
For Serializable and Externalizable classes, the readResolve method allows a class to replace/resolve the object read from the stream before it is returned to the caller.
The method is defined as follows:

```sh
	ANY-ACCESS-MODIFIER Object readResolve() throws ObjectStreamException;
```
	
The readResolve method is called when ObjectInputStream has read an object from the stream and is preparing to return it to the caller. ObjectInputStream checks whether the class of the object defines the readResolve method. If the method is defined, the readResolve method is called to allow the object in the stream to designate the object to be returned. The object returned should be of a type that is compatible with all uses. If it is not compatible, a ClassCastException will be thrown when the type mismatch is discovered.


