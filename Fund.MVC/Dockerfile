FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 3932
EXPOSE 44340

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Fund.MVC/Fund.MVC.csproj", "Fund.MVC/"]
RUN dotnet restore "Fund.MVC/Fund.MVC.csproj"
COPY . .
WORKDIR "/src/Fund.MVC"
RUN dotnet build "Fund.MVC.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Fund.MVC.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Fund.MVC.dll"]