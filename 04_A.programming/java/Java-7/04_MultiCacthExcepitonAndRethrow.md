# Multi Catch Exception Block

	catch (ClassNotFoundException | IOExcepiton e1)

# Rethrow Exception
	1.  the catch block re-throws an exception which is a super-type of declared Exception types,
	2.  the catch block re-throws the exception of type Exception before Java7 we have to Wrap that Exception to throw it back
	