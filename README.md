# docker-registry-web

docker run -v $(pwd)/conf/registry-srv.yml:/etc/docker/registry/config.yml:ro \
           -v /u01/registry:/var/lib/registry \
           -v $(pwd)/conf/auth.cert:/etc/docker/registry/auth.cert:ro -p 5000:5000  \
           --name registry-srv -d registry


docker run -v $(pwd)/conf/registry-web.yml:/conf/config.yml:ro \
           -v $(pwd)/conf/auth.key:/conf/auth.key \
           -v /u01/registry-web:/data \
           -it -p 8080:8080 --link registry-srv --name registry-web daocloud.io/zh_xin/registry-web