# Logout and Last Username

Check this out. Let's fail authentication with a bad password right now. Alright. Two things I notice. One, we have an error. Great. Two, we do not have the user name that I just filled in. Behind the scenes, the authenticator communicates to your security controller by storing things in the session. That's what this authentication [utils 00:00:32] does. If you click, for example, get last authentication error, there's a bunch of code here, but ultimately it's just going out and reading a special key off of this session for the authentication error.

the same thing is true, actually, for get last user name. It just goes on to the session and reads a key off of that session. Now the login for authenticator is already setting the authentication error to the session, but it's not setting the last user name to the session because the base abstract guard form login authenticator doesn't know where you're storing your user name, so all we need to do to get this to work is say, "Request error get session error set." We just need to set that key on the session, and it's stores, and the key is actually stores under a little session, it's the security class, colon, colon, last user name, and of course, our user name is data, underscore, username.

Again, everything has same username but it could be email, it could be anything else. So now, if we try that again ... Good to go. Pre-filled with the [fail 00:01:49] password. Cool. That's done. While we're here. Let's also have one other small, but super important thing, the ability to logout.

Start like normal. In your security controller, let's create a logout action. Here's a handy shortcut I have. We'll say logout action, make this be slash logout and we'll call it security underscore logout. Now, here's the fun part. Don't do anything in here. In fact, throw a new exception that says, this should not be reached. Much like login itself, there's going to be an invisble layer that actually handles logging out. The way that you activate it is, [inaudible 00:02:55], onto your firewall, have a new key called logout. Below that, it's optional, but you can add a path or slash logout.

What this does is it says if the user goes to slash logout, symphony will magically take care of logging them out, which is really cool. Why did we bother creating a controller and a route if Symphony was going to automatically log them out? Because if you don't have a route that responds to slash logout, you'll get a 404, so you still actually need a route. It's just do it a little quirk in Symphony security system, even though the route isn't going to get hit.

The same thing is true for our login route. It's handled by an authenticator, we need to have a route that responds to that URL. It should just work, but let's be friendly and add a logout link. [inaudible 00:03:55] base [inaudible 00:03:55] login link, so let's add a logout link if the user's already logged in. How do we know if the user's logged in? We're going to talk about this more in a second, but you can do an IF statement, for is underscore granted role underscore user. What you may remember is the role we return from the get roles function of user. More on roles later. If they don't have that, then we need to show the login link. if they do have that, let's show them a logout link. Security underscore logout. Perfect.

Let's go back to the homepage. We are anonymous right now. Let's login. ... Cool. It changes to a logout link. Hit logout, back to anonymous. Awesome. Alright. Now, our user probably needs to have a real password.