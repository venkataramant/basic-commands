# Design Patterns

# Categories
	Creational		- How objects are created
	Structure		- How inheritance and composition can be used to provide extra functionality.
	Behavioral		- About communication & assignment responsibilities between objects.

	Creational(5)
		Singleton,Factory,Abstract Factory,Builder,rototype
	Behavior()
		ChainOfResponsibilities,Command,Template


# Creational Patterns
	Singleton
	Factory Method
		- When Application has no idea of the exact type of the objects, it has to work
		- This pattern makes it easy to create those objects indepedently from the rest of the application.
		- Objects implement an "Interface" and Application interacts with the interface.
	Abstract Factory
		- declare interface for each separate products.[Various families of related products]
		- separate "create" method for each interface
		- Abstract Factory returns "Factory" instead of "products"
	Builder
		- Separate creation of an object from its representation.
		- create various "representations" of an objects based upon different "types"(inputs)
		- When Class has many paramters to create
		- Move construction of ojbect logic to a separate class "Builder"
		- final method("build()") returns actual object
		- "Director" defines in which order construction steps to be called and reuse any specific configurations.
		- hides the details of product/object creation from the client code.

	Prototype
		- delegate the object duplication or cloning process to the actual object that are being cloned.
		- a single abstract method interface(SAM)
		- eg "clone()" method
		- Shallow vs Deep copy
		- Objects are referred to same copy (Shallow) [Both original and copy have same values reflected]
		- Prototype Registrary
		- avoids repeated initialization code.
# Behavioral
	Chain of Responsiblity
		- eg : Call center transfers from one repo to another repo
		- transforms particular behaviors/responsibilities into a stand-alone objects ("Handler")
		- Need to execute several handlers in a particular order.
		- allows to update order dynamically.
		- Each handler has to decide to process or pass it to next handler in the chain.
	Command Pattern
		- encapsulates a request as an object [Allows paramaterization to behave differently]
		- Decouple sender and receiver 
	Template Pattern
		- Defines the skelton of an algorithm in the superclass but let's subclasses override specific steps of the algorithm without changing its structure.

	Mediator Pattern
	Memento Pattern
		- enables to save and restore the state of an object without revealing the details of its implementation.
		- Nested Class
		- Orginator class takes the responsiblity of producing snapshots and restoring its state from snapshots.
		- InnerClass Memento class is VTO (value Object)
	Observer Pattern
		- notifies multiple objects/subscribers, about any events that happen to the object they're observing.
		- allows to change or take action on a set of objects when and if the state of another object changes.

	State Pattern
		- allows an object alter its behavior when its internal state changes.
		- context
	Strategy Pattern
	Iterator Pattern
	Visitor Pattern
# Structure Patterns
	Adapter Pattern
	Bridge Pattern
	Composite Pattern
	Decorator
	Facade Pattern
	FlyWeight Pattern
	Proxy Pattern


