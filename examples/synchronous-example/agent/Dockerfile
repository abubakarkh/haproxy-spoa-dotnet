FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /source
COPY HAProxy.StreamProcessingOffload.Agent/ ./HAProxy.StreamProcessingOffload.Agent/
COPY examples/synchronous-example/agent/ ./examples/synchronous-example/agent/
WORKDIR /source/examples/synchronous-example/agent
RUN dotnet build
RUN dotnet publish --configuration Debug -o /output


FROM mcr.microsoft.com/dotnet/core/runtime:2.2
RUN apt update && \
    apt install -y unzip procps && \
    curl -sSL https://aka.ms/getvsdbgsh | /bin/sh /dev/stdin -v latest -l /vsdbg
WORKDIR /app
COPY --from=build /output .
ENTRYPOINT ["dotnet", "Agent.dll"]