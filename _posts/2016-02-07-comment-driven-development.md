---
title: Comment Driven Development
layout: post
category: Software
tags: []
---
As most software methodologies grow from some developer's organizational habit. If the habit helped enough to impact anything significantly, it turns into a method for others to emulate.

Comment driven development is an _extremely simple process_ for breaking apart complex problems into modular (hopefully pure) functions.

<!-- more -->

Begin with the function in question:

```java
public List<Entity> getFilteredEntities(RailRequest request, 
                                        UserGroup group) {
}
```

Next, add comments in the form of a todo list:

```java
public List<Entity> getFilteredEntities(RailRequest request, 
                                        UserGroup group) {
    // validate request using Railroad Auth
    // get user list based on group
    // add users to rail request
    // filter out entities that have 0 accruals
}
```

I've seen this type of function actually fleshed out in a single function. That is a mistake. Functions should do one clear thing wherever possible. Most devs will just tackle the problem and get it done in one massive tangle, but thinking it through this way simplifies and de-clutters--even if it does seem over-optimistic.

Add a code block under each comment or a function call if it will be more than 10 lines.

```java
public List<Entity> getFilteredEntities(RailRequest request, 
                                        UserGroup group) {
    // validate request using Railroad Auth
    if(!isValidRailRequest(request)){
        log.warn("Invalid request");
        return Lists.newArrayList();
    }
    // get user list based on group
    List<Integer> users = database.getUsersByGroup(group);
    // filter out entities that have 0 accruals
    // add users to rail request
    return request.getEntities().stream()
        .filter(x -> !x.getAccruals().equals(0))
        .map(x -> x.addUsers(users))
        .collect(Collectors.toList());
}
```

It's almost painfully simple. There is no magic here. But it does work for me to write out ahead of time what steps need to happen and then make it so. Hopefully it can be of use to you too.