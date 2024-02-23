#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Kodlama.io.Course.WebApiService/Kodlama.io.Course.WebApiService.csproj", "Kodlama.io.Course.WebApiService/"]
RUN dotnet restore "Kodlama.io.Course.WebApiService/Kodlama.io.Course.WebApiService.csproj"
COPY . .
WORKDIR "/src/Kodlama.io.Course.WebApiService"
RUN dotnet build "Kodlama.io.Course.WebApiService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Kodlama.io.Course.WebApiService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Kodlama.io.Course.WebApiService.dll"]