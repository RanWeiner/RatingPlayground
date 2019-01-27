# Playground
Flexible playground with web client that supports posting messages in message board and
rating of elements like movies, TV shows and books. Gain or loose points when rating.

## About this Project
This project was condacted in 5 sprints of two weeks each. 
After those 5 sprints we had two more weeks to finish the [Project Report](Documentation.pdf) and to develop our client. 
We worked in groups of 4 members, organized our sprints assignments with [Trello](https://trello.com) Kanban Board
and used [Bitbucket](https://bitbucket.org) Version Control Repository for our code management.<br />
Our lecturer was <em>Mr. Eisenstein Eyal</em>.

The project was built for academic and study purposes, in Integrative Software Engineering course for Software engineering BSc.
The project goal was to build a server with RESTful API for clients to communicate with.
The API Methods are best described in [here](sprint2.REST.pdf).

### The server development process
We developed our server using [**Spring Framework 5**](https://spring.io/), 
devided to **controller, service** and **dal** components for every system aspect (users, elements, activities).
For our http requests we used [Tomcat](https://tomcat.apache.org/) integrated with springframework.web RestController annotation.<br />
For our database we used [H2](http://www.h2database.com/html/main.html) integrated with springframework.data interfaces 
like [CrudRepository](https://www.baeldung.com/spring-boot-hsqldb) and [PagingAndSortingRepository](https://www.baeldung.com/spring-data-jpa-pagination-sorting) 
that enables you to automatically generate basic SQL queries from your java function name, without a single SQL sentence.

## Features 
#### Users
- The server supports registration and verification (through email address) for new users.<br />
No security measures were implemented, because there were no such requirements from the lecturer.
- Users can choose a role in our playground: **manager**/**player**.<br />
	- Managers can add new elements and update existings elements.<br />
	- Players can play with the elements in the playground.
- All users can update their details, change their role, username etc.<br />
So you will be able to modify elements as manager and use them as player.

#### Elements
- The most important attributes of an element are:
	- expiration date, so players may only play with non expired elements.
	- type, that tells the client what players may do with the element.
	- attributes, a [Map](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) 
	to hold a collection of flexible attributes like image url, or link for more info about the element.
- The client has multiple options for fetching elements from the server:
	- By element identifiers, to fetch a single element.
	- Fetching a list of elements with pagination, so the user could see a page each time and not the entire collection.<br />
	A list can be fetched by:
		- All elements, without any filtering.
		- Distance from point (x,y). Every element also has a location. 
		- Search By attribute, you can search by element name or element type.
		The search is for values that equals your query. We didn't use Like when quering the db.

#### Activities
- Maybe the most interesting feature, Available for players only.<br />
When player wants to 'use' an element, the client offers him options according to the element's type.
- If the element is something that can be rated, the player has two choices: 
	- give this element a rating
	- watch the average rating from all of the playground's players.<br />
The score calculated from proximity of the current rating to the average 
(the formula is written [here](ratingplayground/src/main/java/ratingplayground/plugins/RatingPlugin.java) in <em>calcPoints</em> function),
so players are only allowed to **watch the average if they had already rated it**,
and are allowed to give **one rating per element**.
- The other type we support is a MessageBoard, that players can post messages and view them by pages.
This was a mandatory type for all projects in the course.


## Installation
### Server
In order to run the project with eclipse, please follow these steps:

1. Install [JDK 8](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html), 
[eclipse java EE](https://www.eclipse.org/downloads/packages/) and open eclipse at the root directory.
2. Configure the 3 packages as sources for the project:
	- src/main/java
	- src/main/resources
	- src/test/java
	
###### [jars](jars/):
3. Copy all of our Spring jars [from web.db.lib](jars/web.lib), or download the newer versions.

4. You should have [JavaMail API](https://www.oracle.com/technetwork/java/javamail/index-138643.html)
and [Java Activation Framework](https://www.oracle.com/technetwork/java/jaf11-139815.html) (JAF) installed on your machine:
	- Download the latest versions from the official oracle site
	- Or add both jars from the [from mail.lib](jars/mail.lib) in this repository.

5. Add the mentioned jars to your build path as external jars in eclipse.

6. Run the project as Java Application.
You will find our server running at PORT 8084.

## Technologies
* Spring
	* SpringBootApplication
	* SpringBootTest
	* [Transaction](https://www.baeldung.com/transaction-configuration-with-jpa-and-spring)
	* [Profiles](https://www.baeldung.com/spring-profiles)
	* [AspectJ](https://www.baeldung.com/aspectj)
* H2
* Hibernate
* Jackson
* Stream api
* Tomcat
* Junit
* JavaMail API
* Java Activation Framework (JAF)
* Development Tools
	* Git
		* Bitbucket
	* Eclipse
	* VSCode
	* Trello
