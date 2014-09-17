---
title: Getting Started - Local Data Persistence
page_title: DataSync Getting Started with Local Data Persistence
position: 2
---

# DataSync: Getting Started with Local Data Persistence

The purpose of this article is to demonstrate in a step-by-step manner how you can define the entity classes of your business model, so that you can store data using that model on the device using the SQLite database.


### Defining entity classes


Let's define our entity classes to prepare a sample business model. This operation is simple and you can do it as it is shown below:


	@interface Product : NSObject
		@property (nonatomic) int productID;
		@property (strong, nonatomic) NSString* name;
		@property (strong, nonatomic) NSString* manufacturer;
		@property (strong, nonatomic) NSDate* dateOfPurchase;
		@property (nonatomic) float price;
		@property (nonatomic) long int quantity;
	@end

Note: As you can see, there is no requirement for inheriting from a specific base class, which means that your existing model classes can be easily reused.

Based on the entity class shown above, the ORM engine will automatically create a table named after the entity class name with columns that corresponds to the class properties.


The main class that you need to use as a façade to the **DataSync** component’s functionality is named TKDataSyncContext. You should create one instance that will be bound to one SQLite database and will orchestrate the CRUD (create, read, update, delete) operations and the synchronization process of the tables in this database. The context instance will keep the internal state of data schema and data sets that should be persisted.

The following code demonstrates how to instantiate it and use it for local persistence only.

	TKDataS	yncContext* context = [[TKDataSyncContext alloc] initWithLocalStoreName:@"localDBName" cloudService:nil  syncPolicy:nil];

During initialization of the instance you should specify database name, cloud service client and synchronization policy (see below). In this case we provide **nil** values, because the resulted context will be used for local data persistence only.

Before using the context instance some additional information about the database schema should be set. We should declare the primary key field for all the tables and indices for them if any. You can use tables without explicitly defined indices, but you should never forget to define the primary key field for each one of the tables. **SQLite** does not support composite primary keys, that is why you should make sure that there is a property holding unique values for the entity instances.

In case of a simple ORM usage of the **DataSync** component you can rely on a property of **unsigned long** type with auto incremental behavior, but for complex synchronization process you should ensure the absolute uniqueness of values for all instances of the application. In this case you can use **NSUUID** class or for more complex cases of collaboration you can append **UUID** values with unique identifier of the user. To define a primary key and indices of **Product** table, we use the following method calls:

    [_theContext registerClass:[Product class] //the class of interest
			withPrimaryKeyField:@"productID" 	//the name of property that will be used as PK
			  asAutoincremental:NO]; 			//marks the productID field as auto incremental

    [_theContext registerIndex:@"idxByProductName"  //the name of index
                      forClass:[Product class]		//the class of interest
                     onColumns:@[@"name", @"manufacturer"] //columns included in index. The order is important
                    withOrders:@[@"Asc", @"Desc"]	//sort order for columns
                      asUnique:YES]; 				//uniqueness of the index tuples

As a result of the execution of all the code above, the ORM engine will generate the following schema for Product table:

	CREATE TABLE [Product]
	(
 		[productID] INTEGER PRIMARY KEY AUTOINCREMENT,
	 	[name] VARCHAR,
 		[manufacturer] VARCHAR,
	 	[price] REAL,
 		[quantity] INTEGER,
	 	[dateOfPurchase] REAL
	);
	CREATE UNIQUE INDEX [idxByProductName] ON [Product] (name ASC , manufacturer DESC );

Context methods that should be used for ORM functionality are as follows:

	-(void) insertObject:(id) object; - inserts given object to contexts repository
	-(void) updateObject:(id) object; - marks the given object as updated in context repository
	-(void) deleteObject:(id) object; - marks the given object as deleted in context repository
	-(BOOL) saveChanges:(NSError**) error; - applies to the local database changes that are accumulated in repository
	-(NSNumber*) getScalarWithQuery:(NSString*) scalarQuery failedWithError:(NSError**) error; - this method performs an aggregate query with scalar result bundled in  NSNumber, for example @”Select Count(*) from Product”

	-(NSArray*) getAllObjectsOfType:(Class)type failedWithError:(NSError**) error; - retrieves from database all records of given entity class type materializing them in concrete instances of this type as items of returned array

	-(NSArray*) getObjectsWithQuery: (NSString*) sql
             	withParameters:(NSArray*) parameters
                 	objectType:(Class) objClass
            	failedWithError:(NSError**) error;

The last method is the most advanced one that executes custom parameterized SQL query that meets the **SQLite** requirements for queries. The array with parameters is dynamically bound to an sql string and the returned array keeps records from the database that are materialized in a concrete instances of a given class.

Here is an example of methods reviewed above:

	//insert one product to database
	Product* pd = [self generateNewProduct];
	[self.context insertObject:pd];
	NSError* error = nil;
	if (![self.theContext saveChanges:&error]) {//in case of insertion of many objects, call saveChanges at the very end
	    NSAssert(FALSE, @"Error during persisting of new product:%@", error.description);
	}

	// get all products from databse
	NSError* error = nil;
	NSArray* _products = [self.theContext getAllObjectsOfType:Product.class failedWithError:&error];
	if (!_products){
    	   NSAssert(FALSE, @"Error during persisting of new product:%@", error.description);
	}

	//get all products with price greater than 230
	NSError* error = nil;
	NSArray*  _products = [self.theContext getObjectsWithQuery:@"select * from Product where price > ?"
                                     		 	withParameters:@[@230]
	   				                                 objectType:Product.class
                   					            failedWithError:&error];
	if (!_products){
	      NSAssert(FALSE, @"Error during select query execution:%@", error.description);
	}}
