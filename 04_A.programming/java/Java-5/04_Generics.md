# 


# Variations
	<T> <? extends Parents> <? super Child>
	<?> <? extends T> <? super T>
#  generic type declarations

	1. Class/Interface Declaration with Type Parameters:
		common form of generics in Java, where you declare a class or interface with one or more type parameters.
	
```java
		public class MyClass<T> {
		    // Class implementation
		}
		
```
	2. Method Declaration with Type Parameters:
	declare generic methods within non-generic classes. This allows methods to operate on generic types that may or may not be related to the generic type of the enclosing class.
```java
		public <T> void myMethod(T parameter) {
    // Method implementation
	}
	public <T> T getFirst(List<T> list) {
    return list.isEmpty() ? null : list.get(0);
}
	
```
	3. Bounded Type Parameters:
	Type parameters can have bounds, which restrict the types that can be used as arguments. This can be either an upper bound, a lower bound, or both.
```java
	public class MyClass<T extends Number> {
    // Class implementation
	}
	
	public <T extends Comparable<T>> void myMethod(T parameter) {
	    // Method implementation
	}
	
	public <T extends Number> void processNumbers(List<T> numbers) { /* ... */ }
	public <T super String> void processStrings(List<T> strings) { /* ... */ }
	
	
```
	4. Wildcard Types:
		Wildcards are used to represent unknown types or to specify certain bounds without actually declaring a type parameter.

```java
	Copy code
	public void myMethod(List<?> list) {
	    // Method implementation
	}
	
	public void myMethod(List<? extends Number> list) {
	    // Method implementation
	}
	
	public void processList(List<?> list) { /* ... */ }
	public void processList(List<? extends Number> numbers) { /* ... */ }
	
```
	5. Generic Constructors:
	Like methods, constructors can also be generic.

```java
	Copy code
	public class MyClass<T> {
	    public <U> MyClass(U parameter) {
	        // Constructor implementation
	    }
	}
	public class Pair<K, V> {
    private K key;
    private V value;
    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }
    // Getters and setters
}
```
	6. Generic Interfaces: Interfaces can also be generic.
```java
		public interface Comparable<T> {
		    int compareTo(T o);
		}
```		
	7. Generic Enums: Enums can also be generic.
```java
	public enum Direction {
	    LEFT<Integer>, RIGHT<Integer>, UP<Integer>, DOWN<Integer>;
	}
	
				
```
# method parameters
# wild card
	In Java, you can't directly use a wildcard (?) as a type parameter in a method signature. Wildcards are typically used in generic type declarations, not method parameters.
	
# Advance  Covariance Contravariance invariance
	
	1. Covariance(T) (T and SubTypes) 
		- only type T and subTypes of T are allowed in the context. 
		- Sytanx <E extends T> <? extends T> 
	2. Contravariance(T and SuperTypes) (SuperTypes) 
		- only type T and superTypes of T are allowd in the context
		- Sytanx <E super T> <? super T> 
	3. Invariance(T) (T Type) 
		- only type T and superTypes of T are allowd in the context
		- Sytanx <E super T> <? super T> 
		
			Used when we need to alter the collection  and we need to retrieve the elmenets of the collection.
			
	Arrays 		--> flexible
	Collections --> Compile-time Safety
	Wildcards	--> Both
	Collections and Generics are invariant
	

	method1(Object[] objs) 		  CAN_Accept String[] as inputs
	method2(List<Object> objList) CANNOT_Accept List<String> only accept List<Object>
	method2(List<T> genericList)  CANNOT_Accept List<String> only accept List<Object>
	
# PECS Producer extends and Consumer Super
	When we are passing in a parameter from which we are producing Ts, we want to get Ts out of this parameter, then we should use the type <? extends T> ## get value out of a structure <<covariant>>
	
	When we are passing in a parameter into which we want to put Ts, the thing consumes elements of Type T, then we should use the type <? super T> ## put values into a structure <<Contravariant>>
	
	# dont use wildcard if you want get and put at the same time use <<Invariant>>
	
	# use wildcard if you want using both get and put into the collection

# Wildcard with Return Types
	dont use.
	
	 