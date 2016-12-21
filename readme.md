# Remove App State Lab

This is a small servlet based application that uses the session to store some state.
This is not particularly cloud friendly because the state lives in each app process.
If we scale our app horizontally, then the user will only be logged in if the load balancer
hits the same instance they logged in to.

We can demonstrate this by running two instances of our server, and then running a load balancer in front of them:
in one terminal window run:
`mvn -Dmaven.tomcat.port=8080 -DinstanceNumber=1 tomcat7:run-war`

and in another terminal window run:
`mvn -Dmaven.tomcat.port=9090 -DinstanceNumber=2 tomcat7:run-war`

and in a third window run:
`./start-load-balancer.sh`

Take this example, and introduce a redis server to hold the state.

## Step 2

Now that we have moved our session state in to redis, we can start to take
advantage of the tools that cloud foundry provides- rather than running our
 own instance of redis, we can use the one provided by the platform.
 
 Introduce the spring cloud service connector, and use that to connect to 
 the platform provided redis instance.