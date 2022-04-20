# A Teeny tiny static webpage in docker

This example hosts a tiny static file using `thttpd` executable which is single executable static 
file server.

In this example I executed `thttpd` in following manner:

`thttpd -D -h 0.0.0.0 -p 3000 -d /static-website -u static -l - -M 60`

`-D` launches server in the foreground like a regular program. According to docs this is necessary 
when you want to run `thttpd` wrapped in a little shell script that restarts it if it exits.

`-h 0.0.0.0` server binds to a loopback address

`-p 3000` on port 3000 (which will be exposed from our docker container)

`-d /static-website` the directory which will be served as a static files root dir

`-u static` the username which will need to be created

`-l -` the logfile - here it is not specified so it will spit logs out to STDOUT

`-M 60` the cache-control header

## Starting this tiny static webpage

```shell
docker build -t static:latest .
docker run -it --rm -p 3000:3000 static:latest
```

## Public image

`tomekbielaszewski/tiny-static-webpage:latest`

### Sources

[The smallest Docker image to serve static websites](https://lipanski.com/posts/smallest-docker-image-static-website)