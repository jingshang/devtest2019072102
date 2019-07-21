FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 61317
EXPOSE 44305

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["devtest2019072102/devtest2019072102.csproj", "devtest2019072102/"]
RUN dotnet restore "devtest2019072102/devtest2019072102.csproj"
COPY . .
WORKDIR "/src/devtest2019072102"
RUN dotnet build "devtest2019072102.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "devtest2019072102.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "devtest2019072102.dll"]