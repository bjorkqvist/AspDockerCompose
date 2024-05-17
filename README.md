AspDockerCompose
============
A quite small project with two applications that can start and communicate using docker-compose, with debugging enabled in Rider.

Kinda following https://blog.jetbrains.com/dotnet/2023/08/16/debugging-docker-and-docker-compose-solutions-with-jetbrains-rider/

## Get started

1. Set a debug marker in api in app1.
2. Select docker-compose.yml in list of run configurations and start in debug mode
3. Call api of app, possibly by using .http file AspDockerCompose.http.
