# CF Research

*Install cf CLI*
http://docs.pivotal.io/pivotalcf/1-11/cf-cli/install-go-cli.html 


*For Logging in to PCF* 

`cf login -a _substitute the API endpoint from Apps Manager_ -u _user_ -p _password_`

*For switching between space and organization*

`cf target -s _space-name_`
`cf target -o _organization-name_`

*If facing SSL error*

`cf login -a _substitute the API endpoint from Apps Manager_  --skip-ssl-validation `

*To review current configuration* 

`cf target `

*For Pushing Application* 

1. Navigate to code directory 
  `cf push _app name_ --random-route --no-start =m _memory allocation_ -i_number of instances_`
  
### --no-start is esp usefull when app is required to be bound to services for it to work properly. This way a restage or restart of app is not required

OR 

cf push {app name} -p {jar file or war file} --random-route --no-start =m {memory allocation} -i{number of instances} 


*For starting application*  
cf start {app name}

For vieweing important event for app 
--} app manager --}org space --} application --}Events 

*On cf CLI* 
cf events {app=name} 

*For Tailing logs* 
cf logs {app name} --recent (recent for most recent logs )

### For getting all detailed configuration of apps deployed in cf space and org 
1. Target the space and org
2. cf curl "v2/apps"
3. cf curl "v2/apps/{app metadata.guid}/stats [For detailed stats of the app]

For more details : http://apidocs.cloudfoundry.org 

*For scaling application*
cf scale {appname } -m{memory allocation} -i{ integer - number of instances }
* scaling memory requires restart of application and hence downtime 
* scaling instance doesnt require restart
* PCF auto recovers failing instances of an application


*For creating new service from Marketplace*
cf marketplace
cf create-service {marketplace place service name} {plan} {user service name}  
cf bind-service {appaname} {user service name}
cf restart {appname}

*Converting the app into user provided service*
cf create-user-provided-service {service name/app name} -p {uri}
*uri is the uri for the app restarted in previous step. 

``Manifest can be used to define the bound services, memory, instances, package path location etc 
For creating a manifest from cf cli
cf create-app-manifest {app name} -p {file name } 
*filename = ./manifest.yml ``
  
*For creating log drain service, we need the log drain url of service being used, like splunk, papertrail or laas*

cf create-user-provided-service {log drain service name} -l syslog://{log drain url}
--}bind above service to app 

*Flip activities*

For finding the correct routes of app
cf routes 

*Push the app with different name and different subdomain*

cf push {name v2} -p {package path} -m{memory} -n{subdomain different than current prod} --no-start
bind to required services

cf map-route {name v2} {domain} -n {subdomain prod one}

For removing old version 
cf unmap-route {name v1} {domaine} -n {subdomain}

```
Metrics : http://docs.pivotal.io/pcf-metrics/1-3/using.html```

*To provide particular buildpack during push* 
cf push {appname} -p {package location} -b {buildpack location}

*For setting JRE version* 
cf set-env {appname} JBP_CONFIG_OPEN_JDK_JRE "{jre: { version: 1.8.0_45 }}"
We need to restage app after this change 
cf restage {appname}

*For pushing service broker* 
cf push {app name} ... 

cf set-env {app name} SERVICE_ID {unique id}
cf set-env {app name} SERVICE_NAME {unique Name}
cf set-env {app name} PLAN_ID {plan name}


Start app 
Register the service broker
cf create-service-broker {unique broker name} {username} {passowrd} {url} --space-scoper



*******************************************************************
```Cloud Metrics 

cf list-plugin-repos 
--} to List the available plugins - CF-Community should come up 

to install cf TOP plugin - powerful tool for health monitoring. 
cf install-plugin -r CF-Community "top" 
```

## CF Plugins 

[do-all](https://github.com/ECSTeam/do-all)
```
This plugin can run any cli command for all apps deployed in the particular targetted space.
To install : cf install-plugin do-all -r "CF-Community" 
To run : cf do-all COMMAND ARGS (example : cf do-all restage {} - where {} signifies all applications in targetted space)
```

[top](https://github.com/ECSTeam/cloudfoundry-top-plugin)
```
The best monitoring plugin out there. Shows an interactive view to monitor complete health of Cloud Foundry orgs,space,apps and routes
To install : cf install-plugin -r CF-Community "top"
To run : cf top
```
