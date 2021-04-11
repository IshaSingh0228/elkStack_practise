# SetUp
Search for elastic stack download in google

dld ElasticSearch for windows
dld kibana for windows
dld logstash for windows

unzip the three files

open elasticSearch 
goto bin
start elsearch windows batch file
open browser localhost:9200 to check
copy till bin location 
add in sys variables

similarily do for logstash and kibana


open bin of kibana
open kibana
open browser localhost:5601 to check the server
make sure you are using same version as that of ESearch



copy the logstash.conf file to the logstash folder
open the conf file and change it to
hosts=>["localhost:9260"]

copy the path till bin and open cmd as admin and cd into the path
run : logstash -f ../logstash.conf

Go to browser type the following:
localhost:9200/_cat/indices 
This will show the indices that you created 

stack monitoring>self monitoring>Indices



# Alerting

Link: https://betterprogramming.pub/monitor-your-kubernetes-resources-with-kubewatch-d40ecf420f28

* open slack and launch it
* create an new channeld alert
* skip adding ppl step
* open browse slack and select app mnenu
* search for incoming webhooks and add it
* add to slack
* give ur channel
* add inc webhook integ
* copy the url 

(And paste this in secrets space in elk stack security later stages)


* open elk cloud Link: https://www.elastic.co/cloud/
* start free trial and login with google account
* then create deployment
* general purpose & i/o optimised
* create with default name
* dld the credentials file

* open security in deployment tab in elk cloud
* open keystore
* type this in name
```
xpack.notification.slack.account.monitoring.secure_url
```
* in secret type give the url of slack webhhook and save it



open logstash create a conf file
```
>>
input {
  file {
    type => "java"
    path => "C:/Users/thesi/Desktop/logs/springboot-elk.log"
    start_position => "beginning"
   
  }
}
 

output {
   
  stdout {
    codec => rubydebug
  }
 
  # Sending properly parsed log events to elasticsearch
  elasticsearch {
    hosts => ["https://i-o-optimized-deployment-e4d832.es.westus2.azure.elastic-cloud.com:9243"]
    user => "elastic"
    password =>"90QJ1K6SMBJE7wkIZ8JzTQtq"
   
  }
}
<<
```

give the path for logs
overwrite the hosts part with elastic search's endpoint in the io-deployment tab
add user and password which was dlded from elk cloud
save the conf file and 
run logstash.bat -f logstash2.conf in cmd 

also run the springboot project in sts



open index pattern in kibana
define an index with newly created logstash
@tuimestamp
create index pattern

open kibana > 3 bars > stack management > watcher > create
> create threshold alert >give name > select the indices to query ex.logstash
convert 1000 to 2 in match the following conds
in actions tab select slack and send a sample slack msg to check integration
and create alert

open the localhost:port where the springboot app is running
refresh it 2 times and check if you are getting notified in slack app.