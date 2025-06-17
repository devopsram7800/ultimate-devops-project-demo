## Restore the dependencies STAGE

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
#ARG TARGETARCH
WORKDIR /src
COPY /src/cart ./
COPY /pb/ ./pb/
RUN dotnet restore ./src/cart.csproj 

##BUILD & Publish
#RUN dotnet build ./src/cart.csproj -c Release -o /app/build

RUN dotnet publish ./src/cart.csproj  --no-restore  -o /app/publish

# RUN STAGE

FROM mcr.microsoft.com/dotnet/runtime-deps:8.0-alpine3.20
WORKDIR /src
COPY --from=build /app/publish .

#ENV DOTNET_HOSTBUILDER__RELOADCONFIGONCHANGE=false

EXPOSE 9090
ENTRYPOINT ["./cart"]
