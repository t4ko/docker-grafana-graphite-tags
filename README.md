# docker-grafana-graphite-tags
Docker image to test the experimental graphite's tags functionalities from this repo : https://github.com/DanCech/grafana/tree/graphiteDynamicFunctions

# Build instructions
Use this command to build the image with docker :
```shell
docker build \
    --tag grafana-test \
    --build-arg http_proxy=YOURPROXY \
    --build-arg https_proxy=YOURPROXY \
    --build-arg proxy=YOURPROXY \
    .
```

# Run instructions
1. Create this directory tree to contain the data and configuration files
```
YOURDIR
|--etc
---|--provisioning
------|--datasources
------|--dashboards
```

2. Copy your configuration files in the etc directory

3. Use this command to start the container (default frontend port is 100)
Replace YOURDIR by the directory you created at step 1
```shell
docker run -d --restart always --name grafana-test \
    -p 0.0.0.0:100:3000 \
    -v YOURDIR/etc:/etc/grafana \
    -v YOURDIR:/var/lib/grafana \
    -v YOURDIR/plugins:/var/lib/grafana/plugins \
    grafana-test
```

4. If grafana doesn't start correctly because of a missing file or directory make sure the file and directory permission are correctly set 
