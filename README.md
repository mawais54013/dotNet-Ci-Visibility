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

[Install the Javascript tracer](https://docs.datadoghq.com/tracing/setup_overview/setup/dotnet-core/?tab=windows) 

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
DD_ENV=ci npm test  
```

## Results:
Should be shown in datadog ci after a couple of minutes:
https://app.datadoghq.com/ci/test-runs?index=citest&start=1632627253983&end=1632630853983&paused=false

Working example output:
![image](/test.png)

## Test location:
```
test.js
```

## Documentation
https://docs.datadoghq.com/continuous_integration/setup_tests/javascript/?tab=cucumber
