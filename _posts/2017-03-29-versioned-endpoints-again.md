---
title: Versioned endpoints again
layout: post
categories:
  - Software
---
##tl;dr
  
We're breaking downstream resources because of changing apis.
  
Aside from perfect communication and foresight, the best way to solve this is with versioned apis.

Of the options, I think the **accept header** is best option.

[Troy Hunt -- Your API versioning is wrong](https://www.troyhunt.com/your-api-versioning-is-wrong-which-is/)

##3 options
  
Troy Hunt provides three common methods for versioning apis and points out all the benefits and pitfalls with them all. His article is long, but definitely worth the read if you're interested in these things. This is my summary:

###url

    http://app:9000/app-ws/v1/thing/to/get
    

This is what a few projects at work have used to identify versioned endpoints, and it was the first thing I assumed to be the "right" answer when it came to simplicity. Unfortunately, implementing this method requires a the most code complexity–extra interfaces or copied code, extra logic to handle smart defaults, and non-compliant backwards compatibility with existing endpoints (the ones that don't have the "v1" in the middle of a resource). This method also breaks the rest idea that a url is a location--a version is not a location.

###request header

    http://app:9000/app-ws/thing/to/get
    Headers: "version:1"
    

This method uses a custom defined header that duplicates the purpose of the accept header. This one is hack towards a good idea when the right way to do it is right there in the spec.

###accept header

    http://app:9000/app-ws/thing/to/get
    Accept: application/vnd.app.v1+json
    

When I first saw this method, I actually exclaimed, "that's horrible!" I immediately dismissed it because it's not how I've seen it done. After reading and trying it though, I think it's the best option available.

This method allows for smart default behavior by choosing a default method if the client chooses "application/json" instead. It also allows the client to choose which version it wants without muddying the definition of RESTful endpoints. We want the same location but in a different format (the old format). The best part of all: the code modifications are simple, explicit, non-invasive, and sustainable.

In the following example, getStuffV1 is the default and version 1, while getStuffV2 works for v2. I only added two lines, and they are very clear.

    @POST
    @Produces({"application/json", "application/vnd.stuff.v1+json"})
    @Path("thing/to/get")
    public Response getStuffV1()
    {
    ...
    }
    
    @POST
    @Produces("application/vnd.stuff.v2+json")
    @Path("thing/to/get")
    public Response getStuffV2()
    {
    ...
    }
    

##conclusion
  
I tried to put my conclusion up front. If these simple arguments haven't convinced you, please do some research on it and bring some arguments back. Don't just do the theoretical research either. Build out a resource for each that answers these questions:

  * how simple is it to add a new version server side?
  * how simple is it to update which version my client points to?
  * does versioning with this method encourage bad coding practices?
  * is the concept and implementation clear enough to become widely adopted?