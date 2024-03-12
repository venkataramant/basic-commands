Cloud Resources 4 Hierarchies

Level - 01 (Resources)
		table and bigquery
		storage and buckets
Level - 02 (Projects)

Level -03 Folder and SubFolder

Level -04 Organization Node

--------------------------------------------------------

Policies can be applied at 4 level (* some resources only support policies)

----------------------------------------------
Identity and Access Management

Polices that define "WHO" can do "WHAT" on "WHICH" resources

WHO  -- Principle ---- Email
WHAT -- Role/Permissions (Allow and Deny)

Role::

Basic->
 (Owner/Editor/Viewer/Billing Admin)
Predefined -> 
	Instance Admin Role
Custom -> (manage permissions), can be applied at Project or Organization level Not at Folder Level. 
  Instance Operator (with Predefined Actions):
  	compute.instances.get
  	compute.instances.list
  	compute.instances.start
  	compute.instances.stop
  
WHO -- Principle (Human)
       Service Account (Non-human  Email ID)
       		SA -- Role
       Service Account is also a Resource

Google Account -- Google Groups

>> Cloud Identity
	User can use same login Id/Password in existing Active Directory or LDAP

4 ways Interact with GCP

1. Google Cloud Console
2. Google SDK and Cloud Shell
 	Google Cloud CLI
 	Gcloud storage
 	bq
3. APIs
4. Google Cloud App


