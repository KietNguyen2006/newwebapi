FROM mcr.microsoft.com/dotnet/aspnet:8.0-nanoserver-1809 AS base
WORKDIR /app
EXPOSE 5212

ENV ASPNETCORE_URLS=http://+:5212

FROM mcr.microsoft.com/dotnet/sdk:8.0-nanoserver-1809 AS build
ARG configuration=Release
WORKDIR /src
COPY ["quanlysinhvien.csproj", "./"]


RUN dotnet restore "quanlysinhvien\quanlysinhvien.csproj"
COPY . .
WORKDIR "/src/quanlysinhvien"
RUN dotnet build "quanlysinhvien.csproj" -c $configuration -o /app/build

FROM build AS publish
ARG configuration=Release
RUN dotnet publish "quanlysinhvien.csproj" -c $configuration -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "quanlysinhvien.dll"]
