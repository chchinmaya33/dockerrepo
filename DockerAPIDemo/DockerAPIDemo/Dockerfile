FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["DockerAPIDemo/DockerAPIDemo.csproj", "DockerAPIDemo/"]
RUN dotnet restore "DockerAPIDemo/DockerAPIDemo.csproj"
COPY . .
WORKDIR "/src/DockerAPIDemo"
RUN dotnet build "DockerAPIDemo.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DockerAPIDemo.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerAPIDemo.dll"]