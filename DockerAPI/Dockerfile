# Get base SDK Image from Microsft
FROM mrc.microsoft.com/dotnet/core/sdk:2.2 AS bulid-env 
WORKDIR /app 
#copy the CSPROJ file and restore any dependences (via NUGET)
COPY *.csproj ./
RUN dotnet restore 

# Copy the project files and bulid our releses 
COPY . ./
RUN dotnet publish -c Release -o out 

# Generate runtime image 
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
WORKDIR /app
EXPOSE 80
COPY --from=bulid-env /app/out .
ENTRYPOINT [ "dotnet","DockerAPI.dill"]