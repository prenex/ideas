# Idea

It would be great to have a programming language that is (maybe not even having OOP, but is) having Components.
Close to what I used to do in LightWeightComponents and with XMacros and headers in C/C++.

This should be static binding - at compilation time - and support "dependency injection" at least for
singleton "modules". For "components" - which might be plurally used: for example a "word" in a forth-
like interpreter might be a component - we could use something close to the XMacros.

# Life-cycles?

If these components have life-cycles (or any component life cycles generally), I prefer to have
both an "Awake" and a "Start" call for them. In the awake, the language should forbid reaching data
that is not in our component: that is in the awake we cannot call other components. This ensures that
the Awakes are used for "self-initialization" always! The "Start" callbacks should always happen after
all Awakes and in this one we can call methods/properties/etc or other components. With this setup
there is still a bit chance for getting dependency issues, but at least it forces some good patterns
where it is possible.
Reasoning: In unity it is really a mess when your component's methods get called BEFORE your Awake()
ran and there is no self-initialization. It is very well possible there as the order of Awakes is not
defined clearly (until you make up custom script orders in metadata).

Rem.: Actually it would be best to avoid this problem altogether, but it is not so easy actually!
Rem.: By proper dependency handling and versioning we might avoid the above issues...

# Start components

Also maybe we can circumwent this whole life-cycle topic, by asking the developers to use some main
controller components that manually calls initialization methods. This way a "start component"
need to be defined. This start component will then call and set up every other in the good order.
