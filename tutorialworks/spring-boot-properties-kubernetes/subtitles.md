Hey, it's Tom here at Tutorial Works.

Back with another quick tip for you.

You know that in Spring Boot, properties are the way that we deal with things that can change; like database passwords, or other app settings that you might need, or custom ones that you might provide.

But did you know that you can change the properties of a Spring Boot application at runtime without messing around with all of these properties files and different profiles. 

This trick I'm going to show you is especially useful when you're running it in a cloud environment like Kubernetes.

When you don't want to have to fiddle around with all of these config files.

So let's have a look.

Environment variables, by the way, are depicted by this globe, which I thought looks a bit like the environment!

Firstly, you need to define your property in an application.properties file, as usual.

So in my really serious app here, I'm... going to display my favourite cheese. And I'm going to say it's Camembert.

I've written some code so that it displays that (favourite.cheese). So it uses the @Value annotation to fetch favourite.cheese from application.properties, puts it in a string, and then it will display it as the response from my REST service. So when I run the app it looks like this. That's fairly simple.

But what if you want to display a different cheese when the app is running in Kubernetes.

Or maybe a more practical example would be to change a database password, because you're running your app in production.

Then you can simply override the property with another one.

Now, with Spring Boot there are loads of ways that you can do overrides for properties.

But the one I'm looking at today is environment variables.

So when you're running your app in Kubernetes, you might be running it with a Deployment, which is the thing that creates your Pods.

One of the things you can do on a Deployment is set some custom environment variables on your Pods.

Then when Kubernetes sees those environment variables, it will pick those up and override your current properties with that value.

For an override to work, you need to set a property first.

So if I have a property called favourite.cheese.

Then your environment variable needs to have the same name as your property, but in upper-case characters with underscores.

So favourite.cheese becomes FAVOURITE_CHEESE.

Now I set this environment variable on the Deployment. Here's my Deployment, I just add this 'env' block at the bottom.

I type name for the environment variable and I give it a value.

I can give an explicit value if I want to.

Or, if I'm using a ConfigMap (which you should probably think about doing, if you want to store some application config so you don't hardcode things everywhere), so once you've created a ConfigMap with the key and value you want in it, then you can use the valueFrom instead of an explicit value. 

You type configMapKeyRef, and that tells Kubernetes to look in your ConfigMap for a specific key, and it will fetch the value out of that.

So that's another trick.

And if you don't want to type any of this YAML at all, then the 'kubectl set env' command will do all of it for you, and update the Deployment. So then you can extract that YAML. So you don't need to memorise the syntax.

And once you've done that, voila, your .... oh wait, hang on. It was meant to say Brie. Somehow it now says Cheese in a Can.

My favourite cheese is not Cheese in a Can! So obviously I've done something wrong here.

Yeah. Ugh.

But anyway, this is the end of this video, and probably just time for me to say thank you very much for watching, hope this was useful for you, and hope to see you in the next one. Take care.