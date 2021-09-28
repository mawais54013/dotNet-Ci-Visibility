# Ci-Visibility For .Net
 
## Compatibility 
.NET Core >= 2.1 and >= 3.0 <br/>
.NET >= 5.0 <br/>

Supported test frameworks:

xUnit >= 2.2 <br/>
NUnit >= 3.0 <br/>
MsTest V2 >= 14 <br/>


## Prerequisites
 [Install the Datadog Agent to collect tests data](https://docs.datadoghq.com/continuous_integration/setup_tests/agent/?tab=azurepipelines)

 <br/>
 
Setup vagrant ubunut virtual box: <br/>
https://app.vagrantup.com/ubuntu/boxes/trusty64

<br/> 

[Install the Dot Net tracer](https://docs.datadoghq.com/tracing/setup_overview/setup/dotnet-core/?tab=windows) 

Command:
```
dotnet tool update -g dd-trace
```
## How to Use:
**IMPORTANT NOTE**
<br/>
Recommended to run via vagrant using ubuntu
<br/> 

Run vagrant commands to be in the box
```
vagrant up

vagrant ssh
```
Clone this down:
```
git clone https://github.com/mawais54013/dotNet-Ci-Visibility.git
```
cd into the repo and run command below to install APT:
```
wget https://packages.microsoft.com/config/ubuntu/21.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb
```

Install SDK 3.1 via (if full command below doesn't work, try running them individually):
```
sudo apt-get update; \
  sudo apt-get install -y apt-transport-https && \
  sudo apt-get update && \
  sudo apt-get install -y dotnet-sdk-3.1
```
Install runtime:
```
sudo apt-get update; \
  sudo apt-get install -y apt-transport-https && \
  sudo apt-get update && \
  sudo apt-get install -y aspnetcore-runtime-3.1
```

Install the dotnet tracer via the command below:
```
dotnet tool update -g dd-trace
```

Also install debian package below:
```
curl -LO https://github.com/DataDog/dd-trace-dotnet/releases/download/v1.28.7/datadog-dotnet-apm_1.28.7_amd64.deb
sudo dpkg -i ./datadog-dotnet-apm_1.28.7_amd64.deb

```

**IMPORTANT NOTE** <br/>
If after running the command below you get a "dd-trace" not found, exit and ssh into the vagrant box again and then run the command below

Lastly, run the command below to execute tests:
```
dd-trace --dd-service=my-dotnet-app --dd-env=ci -- dotnet test
```

## Results:
Should be shown in datadog ci after a couple of minutes:
https://app.datadoghq.com/ci/test-runs?index=citest&start=1632627253983&end=1632630853983&paused=false

Working example output:
![image](/test.png)

## Test location:
```
PrimeService.Tests/PrimeService_IsPrimeShould.vb
```

## Documentation
https://docs.datadoghq.com/continuous_integration/setup_tests/dotnet/
