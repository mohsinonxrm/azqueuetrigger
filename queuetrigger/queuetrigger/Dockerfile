FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS installer-env

COPY . /src/dotnet-function-app
RUN cd /src/dotnet-function-app && \
    mkdir -p /home/site/wwwroot && \
    dotnet publish *.csproj --publish linux-arm --output /home/site/wwwroot

FROM mcr.microsoft.com/azure-functions/dotnet:2.0-arm32v7
ENV AzureWebJobsScriptRoot=/home/site/wwwroot \
    AzureFunctionsJobHost__Logging__Console__IsEnabled=true \
	AzureWebJobsStorage=DefaultEndpointsProtocol=https;AccountName=dynamics365af;AccountKey=vO7X74sT8qzuzHzA8CDyP/3Cr7rOsexvx8kD8P5F31Jqjvqy2Z0Kv/DJkGMm/Ql7RJ6R1xhVuvMGam1OFPpJxA==;EndpointSuffix=core.windows.net

COPY --from=installer-env ["/home/site/wwwroot", "/home/site/wwwroot"]