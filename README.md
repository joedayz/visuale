![GitHub tag (latest SemVer)](https://img.shields.io/github/v/tag/Cantara/visuale) ![Build Status](https://jenkins.quadim.ai/buildStatus/icon?job=visuale) [![Project Status: Active – The project has reached a stable, usable state and is being actively developed.](http://www.repostatus.org/badges/latest/active.svg)](http://www.repostatus.org/#active) [![Known Vulnerabilities](https://snyk.io/test/github/Cantara/visuale/badge.svg)](https://snyk.io/test/github/Cantara/visuale)

![Visuale logo](https://raw.githubusercontent.com/Cantara/visuale/master/doc/images/visuale.png)
# Visuale

An real-time dashboard visualisation for real-world micro-service continous deployment environments 

![A shapshot of an early ersion of the visuale dashboard](https://raw.githubusercontent.com/Cantara/visuale/master/doc/images/Visuale-in-action.png)

#### Legend
- battery symbol: SLA/HA quality. Calculated based on the number of healthy nodes weigthed against distributed system norms
- fuel gauge symbol: the node seems to have been running long, meaning that its infrastructure and dependencies may need security patching
- traffic light symbol: the observed heartbeat state of the node, signalling which nodes which are not healthy

## Test yourself
You may have a look and push data at the latest version which is reset frequently here:
* https://visuale.cantara.no/


# Some key targets for the project

- :heavy_check_mark: the UI should mainly be a static UI meant for big-surveilance screens on the walls...  
- :heavy_check_mark: the UI should be continuously updating...   
- :heavy_check_mark: semantic version, running since and some instance info like internal IP are the most important values....    
- :heavy_check_mark: service indicator of the service live resillience/availabillity 
- :heavy_check_mark: a dashboard which display each service (and each service node) with cached/real info ie like what the /health and/or /info endpoint for each service produce.....   
- :heavy_check_mark: the "cluster" instances should be grouped as a service...   
dashboard service... 
- :heavy_check_mark: initial version will be open, i.e. not need any auth... 
- :heavy_check_mark: old/long running services (>7 days) should be marked as insecure/vulnerable due to lack of patching
- :heavy_check_mark: mobile friendly - so you can check your environments on the bus on the way to work 
- :heavy_check_mark: nodes which have not reported for 10 intervals should be marked with a yellow "not working properly" colour...
- :heavy_check_mark: nodes which are not reachable or have missed 50 updates should be marked red/dead...  
- :heavy_check_mark: we will support both pull-based info... and pod/instance CRON jobs which push the health json to the 
- :heavy_check_mark: normal update interval from the service should be 5 or 10 second
- :heavy_check_mark: it might support clicking into a service or a node to see all the details...    
- :white_check_mark: The backend should attempt to do some simple semantic mapping for different json health structures

# Build and test

```
$ mvn clean package
$ java -jar target/visuale.jar
$ wget http://localhost:8088/status/
```

## Configuration

You can add the files you want to poll from Visuale to a file named add_health_resources.txt in the current direcory.

## Docker
```
cd Docker

# Build
sudo docker build -t visuale .

# Run
sudo docker run --rm -p 8080:8080 visuale:latest

# Test - view applocation
wget //http://localhost:8080/

# Let us add some dummy services by using the visuale health itself...
JSON="`wget -qO-  http://localhost:8080/health`";wget --method=PUT --body-data="${JSON}"   http://localhost:8080/status/env/visuale/n1
JSON="`wget -qO-  http://localhost:8080/health`";wget --method=PUT --body-data="${JSON}"   http://localhost:8080/status/env/visuale/n2
JSON="`wget -qO-  http://localhost:8080/health`";wget --method=PUT --body-data="${JSON}"   http://localhost:8080/status/env/visuale/n3
JSON="`wget -qO-  http://localhost:8080/health`";wget --method=PUT --body-data="${JSON}"   http://localhost:8080/status/env/visuale/n4

# Observe the UI gets updated with a new visuale cluster...

```
* Dashboard: http://localhost:8080/
* DockerHub: https://hub.docker.com/r/cantara/visuale


# Some simple agent scripts to push health to visuale

* Look here:  https://github.com/Cantara/visuale/tree/master/agent/scripts


### Visuale on mobile phones

And if you thought this was only for dashboards, we know that time is urgent, so you can check tha status off all your environments conviniently on your phone on your way to work

![A shapshot of an early ersion of the visuale dashboard from a mobile phone](https://raw.githubusercontent.com/Cantara/visuale/master/doc/images/visuale%20on%20mobile.jpg)


