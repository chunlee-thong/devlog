### 20-July-2022

### Getting started

So I was ready to deploy some Dart back-end server using shelf_router to my own Ubuntu server on DO.
Everything is working fine on my local machine (classic programmer quote). So I plan to deploy it using a docker container. I'm lazy to use `docker compose`, so just plain docker build and run is enough.
I set up the Nginx config file and domain name, and everything is perfect.
I don't set up any webhook to automatic deploy or something. I thought this was just a one-go and done.

### Problems

After everything is set up. I send a POST request from my local machine using Postman to the server's endpoint.
I receive a 400 error code with the error message that I'm familiar enough with that is related to jsonDecode (I decode and encode JSON from File).
To know more about what's going on, I update the code and dump the stack trace to the response.

### Re-deploy count

1. After re-deploy and sending a request again, Looks like I have an error when decoding a request body to Map (shelf_router request body returns a string, so I have to decode it to Map).
2. My first thought is must be some error with decoding or something with the shelf_router `readAsString` method to read a request body. I specified the encoding to uft8 and redeploy it again.
3. Same error still occur, So I add a code to log a request body and re-deploy again.
4. I check the log and turn out that the request body is empty. I check my Postman setting and headers. Nothing is wrong or weird going on. I google about the issue but nothing comes up.
So I thought this must be some problem related to Docker or something related to my environment. Well, I run my project as a Docker container on my local machine, and turn out there is no issue with it.
Well if Docker isn't a problem, a deeper layer must be related to Nginx.
So I google some problems related to Dart and Nginx and come across this [stackoverflow question](https://stackoverflow.com/questions/70658066/nginx-as-proxy-for-dart-server-does-not-pass-post-request-body).
I tried the accepted answer that was posted by OP and BOOM, it works. I shake my head and start laughing.

### Conclusion

I think this is the kind of moment that makes me enjoy my programming career.
This is a mix of emotions of frustration, happiness, and unexpected.. so that's why I decide to create a Devlog about this.
This comes up so soon that I will just post it here publicly on Github.

