FROM 192.168.161.151/coresdk/aspnetcore AS base
WORKDIR /app
EXPOSE 5001

FROM 192.168.161.151/coresdk/aspnetcore-build AS build
WORKDIR /src
COPY . .
RUN dotnet restore
WORKDIR /src
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplication1.dll"]