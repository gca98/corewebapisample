

#FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
#WORKDIR /app
#EXPOSE 80
#EXPOSE 443
#
#FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
#WORKDIR /src
#COPY ["CoreWebApiHEROKU/CoreWebApiHEROKU.csproj", "CoreWebApiHEROKU/"]
#RUN dotnet restore "CoreWebApiHEROKU/CoreWebApiHEROKU.csproj"
#COPY . .
#WORKDIR "/src/CoreWebApiHEROKU"
#RUN dotnet build "CoreWebApiHEROKU.csproj" -c Release -o /app/build
#
#FROM build AS publish
#RUN dotnet publish "CoreWebApiHEROKU.csproj" -c Release -o /app/publish
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "CoreWebApiHEROKU.dll"]


FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
EXPOSE 48719
EXPOSE 27017
EXPOSE 5000
EXPOSE 5001

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ..

#COPY ["CoreWebApi/CoreWebApi.csproj", "CoreWebApi/"]
#RUN dotnet restore "CoreWebApi/CoreWebApi.csproj"
#COPY . .
#WORKDIR "/src/CoreWebApi"
#RUN dotnet build "CoreWebApi.csproj" -c Release -o /app/build

RUN dotnet restore 
RUN dotnet build --no-restore -c Release -o /app

FROM build AS publish
RUN dotnet publish "CoreWebApiHEROKU.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
#COPY --from=publish /app/publish .
COPY --from=publish /app/ .
#ENTRYPOINT ["dotnet", "CoreWebApi.dll"]
CMD ASPNETCORE_URLS=http://*:$PORT dotnet CoreWebApiHEROKU.dll