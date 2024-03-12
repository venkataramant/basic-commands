# Architecure patterns 
	Patterns help define the basic characteristics and behavior of an application.
	Does the architecture scale
	What are performance characteristics of the application
	How easily does the applicatin respond to change
	What are the deployment characteristics of the application

# N-tier Architecture (Layered Architecture)
	big ball of mud architecture anti-pattern
	Components within the layered architecture patterns are organized into horizontal layers, each one of performing a particular role/set of tasks within the application.[ Presentation layer, business layer, peristence, and database]

	Layers of Separation::
		Strength of this pattern is the separation of concerns among components. A closed layer means that as a request move from layer to layer, it must go throughthe layer right below it to get to next layer below that one. 
	Architecture sinkhole anti-pattern:
		Where requests flow through multiple layers of the architecture as simple pass-through processing with little or no logic performed within each layer.
	Monolithic application behavior

	low:
	 	Overall agility,Ease of Deployment*,Performance,Scalability
	High:
		Ease of development,Testability

# Event-Driven Architecture
	A popular distributed asynchronous architecture apptern to create high scalable applications. Highly decoupled,single-purpose event processing components that asynchronously receive and process the events.

	2 Main topoloiges: [ Mediator and Broker]
		Event Mediator
			To orchestrate multiple steps within an event through a central mediator.It is useful for events that have multiple steps and require some level of orchestration to process the event.
				4 Main architecture components:
					Event Queues [Initial events]
					Event Mediator
					Event Channels [Processing events]
					Event Processors
				https://towardsdatascience.com/event-driven-architecture-pattern-b54fc50276cd
		Broker
		    To chain events together without use of a central mediator.





# 