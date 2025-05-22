FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build-backend
WORKDIR /app

# Install Node.js
RUN apt-get update && \
    apt-get install -y curl && \
    curl -fsSL https://deb.nodesource.com/setup_22.x | bash - && \
    apt-get install -y nodejs

COPY . ./

RUN dotnet publish ./CommentApp.csproj -c Release -o out

FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS runtime
WORKDIR /app
COPY --from=build-backend /app/out ./
ENTRYPOINT ["dotnet", "CommentApp.dll"]