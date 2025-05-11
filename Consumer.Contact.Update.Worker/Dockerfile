FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Consumer.Contact.Update.Worker/Consumer.Contact.Update.Worker.csproj", "Consumer.Contact.Update.Worker/"]
COPY ["Consumer.Contact.Update.Domain/Consumer.Contact.Update.Domain.csproj", "Consumer.Contact.Update.Domain/"]
COPY ["Consumer.Contact.Update.Infrastructure/Consumer.Contact.Update.Infrastructure.csproj", "Consumer.Contact.Update.Infrastructure/"]
COPY ["Consumer.Contact.Update.Service/Consumer.Contact.Update.Service.csproj", "Consumer.Contact.Update.Service/"]
RUN dotnet restore "Consumer.Contact.Update.Worker/Consumer.Contact.Update.Worker.csproj"
COPY . .
WORKDIR "/src/Consumer.Contact.Update.Worker"
RUN dotnet build -c Release -o /app/build
RUN dotnet publish -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENV ASPNETCORE_URLS=http://+:80
ENTRYPOINT ["dotnet", "Consumer.Contact.Update.Worker.dll"]
