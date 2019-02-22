FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["MemcachedMvc/MemcachedMvc.csproj", "MemcachedMvc/"]
RUN dotnet restore "MemcachedMvc/MemcachedMvc.csproj"
COPY . .
WORKDIR "/src/MemcachedMvc"
RUN dotnet build "MemcachedMvc.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MemcachedMvc.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MemcachedMvc.dll"]