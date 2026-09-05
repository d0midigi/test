# Hacking Web Applications

Hacking Web Applications

In any organization there exists a diverse portfolio of applications that support the normal functionalities and operations of the client enterprise. These applications are responsible for delivering the critical services and information the client organization needs to make their business works and support their mission whatever it may be. In today’s business environment these services are being delivered to increasing amounts of clients via what are known as web applications. Web applications are coded software that is utilized over a network connection such as the Internet. Usually, they are accessed via web browser and use technologies to aid in their functions such as Java, ActiveX, Silverlight, Flash, and JavaScript, to name a few. Web applications are used to deliver services needed to run operations of businesses over the web, moving the processing of data and other functions either wholly or partially off of the client to the server or a mix of the two.

With the increasing use of these applications, security remains the focal point of an insecure web application that could lead to unintended consequences and without proper defensive measures in place, they must be considered. Interference with or tampering of a web application could have catastrophic consequences including disclosure of or modification of customer data for example. Other types of attacks could even include taking the application offline through the use of Denial of Service (DoS) or Distributed Denial of Service (DDoS) type attacks.

The key to securing web applications is knowing what they are, how they function, and the various components involved. In this chapter we will examine the environment web applications and their clients from attack.

**Understanding Web Applications**

Web applications, in terms of software engineering, are any service or software that is commonly delivered to the client from a web server over a network. Applications that fit this definition typically are those that are delivered over the web or intranet to a web browser or in some cases a specially designed client application. These types of applications have become very popular for a number of reasons including the ability to centrally manage and maintain an application thereby eliminating many of the headaches that are present when applications have to be updated on multiple systems. They are also favored due to the fact that maintenance behind gone to upgrade or update these applications does not always impact the end user utilizing them.

Additionally, these types of software applications are popular because they make it possible to install what are known as _**thin clients**_ which are very minimalistic software applications. Thin clients are a common software device that becomes possible in the case of web applications due in part to processing being moved in whole or in part to the server meaning lesser processing requirements on the client. A commonly used thin client is a web browser. Thin clients on the desktop side can be as simple as having a web browser with the appropriate plug-ins or as complex as having a dedicated piece of software that interacts with the web application. The figure below shows how web applications commonly work over the Internet. You can see from this example that an attacker can perform many attacks, for example, sending the client to a malicious web server, or XXS, or SQLi, session hijacking, or HTTP Response Splitting, as examples.

In the case of web applications there are many variations that are only limited by the creativity and skill of the developer or designer. One of the more common variations includes the well-known multitiered application. IN this configuration some of the well-known tiers are the server-side web server in the first tier, the web application itself in the second tier (also known as middleware), and the data or database itself in the third tier. The figure below also shows an example of a commonly used 3-tier web application.

The interactions between the client, the tiers, and these components works as such:

1. A client wishes to access their banking information online. They open a web browser and go to the bank of their choice using the public Internet. The browser sends requests to the server and web application. In other words, the first tier sends requests to the middle or second tier. The first tier is commonly homed with web servers such as Apache or IIS and they should be load balanced accordingly. The web server accepts your request, and you can then interact with the banking software.

![](<../.gitbook/assets/0 (37).png>)

_**FIGURE X:** A high-level view of how web applications work._

**NOTE: Commonly encountered and used web applications include all forms of webmail, Microsoft’s SharePoint, e-commerce applications, discussion group forums, and many others.**

1. A client then enters their login information and is able to process their banking requests. Normally, depending on what they are doing, the second tier software (or middleware) is processing those requests and accessing the third tier as necessary. For example, your request to see a history of your latest transactions. Normally, the middleware servers are also redundant, keep state and allow for the handoff back to the web servers in the first tier and then the client’s web browser processing the requests.

![](<../.gitbook/assets/1 (23).png>)

_**FIGURE X:** An example of a 3-Tier web application._

1. The middle or second tier then accepts these requests and send them on to the last or third tier in the form of a query that interacts with the database either returning information as requested or, in some cases, performing some sort of update to the database as required.
2. The client accesses the bank website and has a fully functional experience not knowing (since its transparent to them) that multiple tiers of servers processed the requests, gathered the information and held state in cases where a shopping cart was used as an example.

So now that we understand what platform a web application is kept on, let’s look at some of the finer details of the tiers. Notice how the information ultimately is stored and queried from a database? Traditional applications before being converted to web applications ultimately access a database of some type to use its stored data. Since most users use the Internet and a web browser to access this data, the trend over the last several years is to move some of the traditional, single user applications to a multiuse environment and then to the web.

**NOTE: State is held so that if your session is abnormally terminated or a server fails, your experience stays the same. By re-accessing the site, you will be able to continue shopping, or a failed server will be transparent to you, the user of the web application. This is one of the many reasons why web applications are now used more than every in today’s environments especially when utilized over the public Internet.**

The increased adoption of networks and networking into new environments as well as traditional technologies being used in new ways has prompted developers to include web interfaces for their traditional apps. This is essentially what grew the need for other tiers such as web access over web servers and middleware for business logic. Regardless, the client accessing the solution or platform is the same, it’s commonly a web browser that suffers from client-side attacks, such as XSS and DoS attacks.

Applications that used to be something that was hosted locally on a client have now been migrated or upgraded to be a web application. Some companies have even moved towards web-based applications as a means of instituting a pay-as-you-go model where users do not purchase the application as they would traditionally, but instead pay only for the time they are using it in a subscription-based format. Companies that practice this software delivery model have led to the rise of the term _**Application Service Provider**_, or ASP.

**DID YOU KNOW: A good example of a client platform as well as a form of thin client can be any number of smartphones that exist on the market today. Many of these smartphones, for example the iPhone, access information from a server via an interface on the device, such as any one of the number of apps on the iPhone. These types of devices do not host any, or hold very little information locally, instead they host it remotely on a server where the applets (lightweight applications) present an interface to the user to interact with and make requests through.**

**This type of environment shows us that client-side attacks have the potential to effect not just desktop computers, but other non-traditional devices as well.**

ASPs are currently receiving much attention in the software industry due to their ability to host applications on their servers and perform the maintenance and upgrades for a client therefore offloading some duties to a third-party. An increasing number of software companies are choosing to go the route of using web applications instead of single-use applications due to the increased flexibility and ease of maintenance so as security professionals and ethical hackers we need to learn about them quickly, find their weaknesses, educate our clients, and learn how to mitigate the attacks.

**Types of Web Applications**

Many different types of web applications exist in today’s world all of which are found on both the individual and home environment all the way up to and including the enterprise. The technologies used to create rich and useful applications rests in the various types of components that allow for dynamic content to be created.

Dynamic content is content that can change and process data as well as render it to the client in different ways. Many technologies exist that can do this for the client and the web developer, such as Java, JavaScript, ActiveX, Jscript, ActionScript, Flash, Silverlight, VBScript, and so on. These technologies all have inherent risks, especially when used to produce and deliver web applications over the Internet.

**Microsoft ActiveX**

When developing a web application, many will find ActiveX to be one of the most commonly used tools today. Developers find that most browsers on the market are trumped by the use of Microsoft’s Bing web browser. It is also true that not only is Microsoft’s browser the most commonly used, but it also ties in directly with the base operating system, all of the NOS systems, all of the BackOrifice products such as SharePoint and Microsoft Exchange, the Microsoft desktop productivity suite called Office and any and all other Microsoft products available. Because of its widespread use, ignoring ActiveX would limit most vendors, developers and companies to a smaller market. That being said, ActiveX also became an open technology allowing more developers to work with it, ties nicely into Adobe’s products and functions on most web browsers in use today with the add-in’s, plug-ins, and development kits available on the market.

ActiveX controls are a technology that Microsoft has positioned as their part of their suite of web development technologies and as such is heavily represented in their own applications as well as many third-party packages. Technology has grown quite rapidly in the past 15 or so years. It has been around and has become something that is present on seemingly every website around rendering content such as streaming video, media, images, and many other types of content.
