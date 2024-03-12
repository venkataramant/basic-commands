# Annotations
	java.lang.annotations.Annotations
	

	
	1. Code Generation - To generate boilerplate code for things like getters,setters and constructors
	2. Compile-time Checking - to detect errors or suppress warning
	3. Runtime processing: to provide information or to alter the behavior of
	4. Tools
# Examples
		@Override
		@Deprecated
		@SuppressWarnings("deprecation")
		
	Target
	Retention
		RetentionPolicy.SOURCE (Code is generated and discarded)
		RetentionPolicy.CLASS  (Part of Class/Code, not available at Runtime)
		RetentionPolicy.RUNTIME (Available at Runtime through reflections)
# Annotation Types
	Maker Annotations
		No variables
	Single Member Annotations
		We can pass value without name of member name
		When multiple members with default values except one variable
# Custom Annotaitons

'''java
	import java.lang.annotation.Retention;
	import java.lang.annotation.RetentionPolicy;
	public @interface MyRuntimeAnnotations{
		String myName();
		int myValue();
	}
'''
# Adding Static variables

	Adding any new proper variable make it  final & static by default.

# Passing Array as values
	items = {} // Empty Array
	items = {1,2,3}
	items = 1 //Compiler will add missing braces
# Annotations to Annotations
	@Repeatable(MyAnnotation.class) [Container Annotation]
	@Inherited
	@Docuemented
	@Retention
	@Target
		ElementType.TYPE,
		ElementType.FIELD,
		ElementType.METHOD,
		ElementType.PARAMETER,
		ElementType.CONSTRUCTOR,
		ElementType.LOCAL_VARIABLE,
		ElementType.ANNOTATION_TYPE,
		ElementType.PACKAGE 

    /**
     * @since 1.8
     */
    ElementType.TYPE_PARAMETER
    ElementType.TYPE_USE,

    /**
     * @since 9
     */
    ElementType.MODULE

    /**
     * @since 16
     */
    ElementType.RECORD_COMPONENT;
	
# Important Methods
	java.lang.Class.getAnnotatedInterfaces();
	java.lang.Class.getAnnotatedSuperclass();
	java.lang.Class.getAnnotation(ANN.class);
	java.lang.Class.getAnnotations();
	java.lang.Class.getAnnotationsByType(TypeClass);
	
	java.lang.reflect.Method.getAnnotatedExceptionTypes();
	java.lang.reflect.Method.getAnnotatedParameterTypes();
	java.lang.reflect.Method.getAnnotatedReceiverType();
	java.lang.reflect.Method.getAnnotatedReturnType();
	java.lang.reflect.Method.getAnnotation(ANN.class);
	java.lang.reflect.Method.getAnnotations();
	java.lang.reflect.Method.getAnnotationsByType(null)
	java.lang.reflect.Method.getDeclaredAnnotation(Class.Type)
	java.lang.reflect.Method.getDeclaredAnnotations();
	java.lang.reflect.Method.getDeclaredAnnotationsByType(Class.Type)