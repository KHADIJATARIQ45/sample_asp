#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM microsoft/aspnetcore:1.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:1.0 AS build
WORKDIR /src
COPY ["demoaks/demoaks.csproj", "demoaks/"]
RUN dotnet restore "demoaks/demoaks.csproj"
COPY . .
WORKDIR "/src/demoaks"
RUN dotnet build "demoaks.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "demoaks.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "demoaks.dll"]