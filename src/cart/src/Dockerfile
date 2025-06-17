## Restore the dependencies STAGE

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY /src/cart ./
COPY /pb/ ./pb/
RUN dotnet restore ./src/cart.csproj 

##BUILD & Publish
RUN dotnet build ./src/cart.csproj -c Release -o /app/build

RUN dotnet publish ./src/cart.csproj - Release -o /app/publish

# RUN STAGE

FROM mcr.microsoft.com/dotnet/sdk:8.0 
WORKDIR /src
COPY --from=build /app/publish .
EXPOSE 9090
ENTRYPOINT ["./cart"]
