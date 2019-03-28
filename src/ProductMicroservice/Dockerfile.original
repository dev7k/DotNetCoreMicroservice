FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["src/ProductMicroservice/ProductMicroservice.csproj", "src/ProductMicroservice/"]
RUN dotnet restore "src/ProductMicroservice/ProductMicroservice.csproj"
COPY . .
WORKDIR "/src/src/ProductMicroservice"
RUN dotnet build "ProductMicroservice.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ProductMicroservice.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ProductMicroservice.dll"]