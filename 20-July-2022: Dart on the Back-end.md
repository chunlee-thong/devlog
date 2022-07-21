
### Getting started

So I was ready to deploy some Dart back-end server using shelf_router to my own ubuntu server on DO.
Everything is working fine on my local machine (classic programmer quote). So I plan to deploy it using a docker container. I'm lazy to use docker compose, so just plain docker build and run is enough.
I setup nginx config file and domain name, everything is perfect.
I don't setup any webhook to automatic deploy or something. I thought this just a one go and done.

### Problems

After everything is setup. I send a POST request from my local machine using Postman to server's endpoint.
I receive a 400 error code and with error message that i'm familiar enough that is relate to jsonDecode (I decode and encode json from File).
To know more what's going on, I update the code and dump the stacktrace to the response.

### Re-deploy count

1. After re-deploy and send a request again, Looks like I have an error when decode a request body to Map (shelf_router request body return a string, so i have to decode it to Map).
2. My first thought is must be some error with decoding or something with shelf_router `readAsString` method to read a request body. I specified the encoding to uft8 and redeploy again.
3. Same error still occur, So I add a code to log a request body and re-deploy again.
4. I check the log and turn out that request body is empty. I check my Postman setting and headers. Nothing is wrong or weird going on. I google about the issue but nothing comes up.
So I thought this must be some problem related to Docker or something relate to my environment. Well, I run my project as a Docker container on my Local machine and turn out there is no issue with it.
Well if Docker isn't a problem, a deeper layer must be related to Nginx.
So I google some problem related to Dart and Nginx and come accross with [stackoverflow question](https://stackoverflow.com/questions/70658066/nginx-as-proxy-for-dart-server-does-not-pass-post-request-body).
I tried the accepted answer that was post by OP and BOOM, it works. I shake my head and start laughing.

### Conclusion

I think this is the kind of moment that make me enjoy my programming career.
This is a mix emotion of frustation, hapiness, unexpected.. so that's why i decide to create a devlog about this.
This come up so soon that i will just post it here publicly on Github.

