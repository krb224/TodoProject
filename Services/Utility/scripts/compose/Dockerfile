FROM microsoft/aspnetcore-build:2.0 AS build-env
WORKDIR /app

# Copy everything else and build
COPY . ./
RUN dotnet restore
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/aspnetcore:2.0
WORKDIR /app
COPY --from=build-env /app/**/out ./
COPY ./entry.sh .
RUN chmod +x ./entry.sh
CMD /bin/bash ./entry.sh
