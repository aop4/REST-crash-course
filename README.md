# REST-crash-course

These notes follow along with the presentation slides in the repository. Sections are numbered according to the corresponding slide number.  

**2. Developers need the internet.**  
Most useful software today utilizes the internet. Mobile applications, video games, and even Microsoft Word access the web. Thus, leveraging the web is simply a fact of life for most software engineers.  

**3. The internet is being used for a continuously growing range of devices and applications.**  
As technology evolves, we have put ever increasing demands on our web-based systems. Back end servers (generally responsible for data storage and manipulation) have to communicate with a growing array of devices, from phones to AR headsets to televisions and those annoying little talking things you put on your bedside table. When we were just serving content to personal computers, there wasn’t a huge need to create a back end that was portable--the back end could stay very closely tied to the front end, or the code responsible for formatting and displaying content. Today, this is not the case. It saves time, money, and resources to have a single back end that can serve all of these devices, no matter how they convey content to the user. REST helps us achieve this separation of server-side and client-side code in an organized manner.  

**A simplified view: The internet is for information transfer.** We can say that, for the most part, web technologies function as follows: user devices make a *request* to the server either to obtain new information or to modify information stored at the back end. That request is met with a *response* from the server. The response contains the information that was requested and/or a status code indicating whether there was success or an error was encountered.

**4. What do you mean by "information," exactly?**  
But what kind of data is being passed back and forth? It’s very frequently data like the JSON object pictured on slide 4. XML and HTML are also ways to transfer data, and still other kinds of files can be sent with a response.  

**5. REST (Representational State Transfer)**  
REST is an architectural style for communication over the internet created by Roy Fielding of UC Irvine in 2000. It’s actually quite remarkable that a PhD student (and not a full-fledged professor or industry veteran) came up with REST, because it's now wildly popular in industry. If you’re looking for a software engineering gig these days, familiarity with REST APIs is very frequently one of the “requirements,” or at least “desired” in a good candidate. So listen up!  

**6. REST constraints**  
As stated before, one of the key aspects of the REST architecture is that it requires us to separate client side and server side code completely. This allows us to overhaul the UI (which seems to be completely rebuilt all the time today) and accommodate new devices easily.  
REST is also a *stateless* architecture. This means that the client side is responsible for sending all context the server needs to understand a given request… and so the server doesn’t need to store anything extra for an active user.  
The server is also supposed to indicate whether data in a response can be cached. For example, images and audio files can be cached (saved) in a user’s web browser in order to decrease unnecessary loading times for the user and to lower demand on the server. But we wouldn’t want to cache a student’s course listing because it’s subject to change over time, and this could lead to very angry users.  
A REST system is also a layered system, meaning that there may be multiple servers at the backend for load-balancing and organizational reasons, but this won’t be apparent in the client-side code at all (i.e., no adjustments need to be made on the client side).  

**7. REST... for developers**  
A key abstraction in REST is the idea of “resources.” In Fielding’s PhD thesis, he essentially says a resource is any data you can give a name. It might be a user in the database, a list of users in the database, or an image. The way we represent this data (file formats, etc.) is also not restricted under REST.  

Now for the fun stuff. A key part of a good REST API is the appropriate use of HTTP methods. The most common methods are GET, POST, PUT, and DELETE, and if you want to do things right, you really should go beyond GET and POST.  
GET is generally used to request a resource (data) from the server, PUT to modify data at the back end, DELETE to delete data, and POST to create new data or do something the other verbs don’t quite describe. Remember: it's the client side that's asking the server to do these things, by invoking the proper method.  

**8. The combination of HTTP method and URI describes what a call to the API is doing.**  
Ideally, the URIs used to interact with resources are structured in a certain way. Slide 8 provides some examples of how this might work. Instead of having separate URLs for each of the operations shown (say /users/all, /users/delete, /users/new, /users/change...*please* don’t do that), we can have just two URL paths and rely on the HTTP methods to communicate what it is that you’re trying to do. One benefit of this is having to maintain fewer URL paths, but it also makes it easy to understand what a given piece of code at the back or front end is intended to do. REST enforces a sort of contract between the back and front end through URI path and HTTP method choices.  

**9. Using informative error statuses**  
Another aspect of a good REST API is sending an informative error status to the client-side when things go wrong and sending the correct success status when they go all right. There is a long list of HTTP status codes, and sometimes figuring out which to use is a bit of an art, but the community of REST API builders has come to a consenus on a lot of common scenarios. For example, if we’re requesting a JSON object with user 22’s information and can’t find that user, we should send back a 404 error (just like when a web page can’t be found).  

**10. [Django REST Framework example]**  
Slide 10 gives you some idea of what a REST API might look like at the back end. This particular get() method is called, in my example code, when the client sends a GET request to the url `<site-domainb>/students/<id>`. The line `student = Student.objects.filter(id=id).first()` tries to pull the user with the ID passed in as part of the URL from the database. (One of the beautiful things about Django, Ruby on Rails, and other MVC frameworks is that we don’t need to write SQL to interact with the database.) If the student can’t be found, a 404 error status is returned, but if they can be found, we serialize the student as a JSON object and send the object back to the client with the default HTTP status 200 (OK).  

**11. Further Reading**  
If that example using the Django REST Framework piques your interest, I set up some starter code that should get you up and running with a local database and a codebase to build off of at <https://github.com/aop4/heroku-django-REST-template>. I *think* it’s possible to get it running in under 10 minutes. I also recommend the resources on slide 11 as further reading.  
