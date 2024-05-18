AspDockerCompose
============
A quite small project with two asp applications that can start and communicate using docker-compose, with debugging enabled in Rider.

Kinda following https://blog.jetbrains.com/dotnet/2023/08/16/debugging-docker-and-docker-compose-solutions-with-jetbrains-rider/

## Get started
1. Set a debug marker in api in app1.
2. Select docker-compose.yml in list of run configurations and start in debug mode
3. Call api of app1, possibly by using .http file AspDockerCompose.App1.http.
4. Enjoy your debugging session :)

Of course, you can also start the applications using
```
docker compose up
```
But I don't think debugging in Rider is working that way.

## Notes on compose networking
Note that all containers in the compose file are added to a docker network that they can use to communicate.
When calling from one container to another in a compose setup, the service name should be used, e.g. like this

```
HttpClient client = new();
var forecast = await client.GetFromJsonAsync<WeatherForecast[]>("http://aspdockercompose_app2:8080/weatherforecastapp2");
return forecast;
```

But when app2 is called from host environment (possibly by using Postman, AspDockerCompose.App2.http or running App1 with dotnet run)
the HOST_PORT defined to the left in docker-compose.yml should be used, e.g.
```
@AspDockerCompose.App2_HostAddress = http://localhost:2222

GET {{AspDockerCompose.App2_HostAddress}}/weatherforecast/
Accept: application/json

###

```


## Resources
https://blog.jetbrains.com/dotnet/2023/08/16/debugging-docker-and-docker-compose-solutions-with-jetbrains-rider/

https://www.jetbrains.com/help/rider/docker_compose.html#create-docker-compose-run-configuration

https://www.yogihosting.com/docker-compose-aspnet-core/

https://docs.docker.com/compose/networking/


