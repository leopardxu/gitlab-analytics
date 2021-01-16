# gitlab-analytics 

### changes

* 修改了mysql root 密码，连接使用root 用户,降低使用难度;
* 修改默认python 源==》https://mirrors.aliyun.com/pypi/simple，更适合国人使用；
* 实在构建不出来 ga 镜像的话，可以 docker pull leopardxu/ga ; docker tag leopardxu/ga:latest ga:latest ；
* 第一次启动用docker-compose up mysql grafana ga 可以看到日志，方便查看启动问题；
* 正式用 docker-compose up -d mysql grafana ga；
* 通过ip:8080 访问下发webhook 页面： 需要配置gitlabURL 以及用户token（最好是admin级别的），下发hook挺方便的；
* 通过ip:3000 查看grafana页面（注意首次查看没有数据，数据是从hook下发后才开始收集的）；
* 通过grafana的 dashboard，可以督促大家正确的使用gitlab~~~ ；

### Goals
* Improve the developers' enthusiasm to build more standard gitlab's project. 
* Provide a guidance to the developers for gitlab's features. 
* Analysis the activity of gitlab's users via statistics.
* Support kpi's measurement for project managers.

### Analytics
* commits
* wikis
* issues
* comments
* merge-requests

# Installation

### Initialize with Docker

```shell
git clone https://github.com/NDHWAlliance/gitlab-analytics.git
cd gitlab-analytics
docker-compose up mysql grafana ga
```

If you are a Chinese user, you can use following commands to speed up `ga` image
build process;

```shell
git clone https://github.com/NDHWAlliance/gitlab-analytics.git
cd gitlab-analytics
docker-compose build --build-arg INDEX_URL=https://mirrors.aliyun.com/pypi/simple ga
docker-compose up -d mysql grafana ga
```
 
### Configuration
* Step 1: Access flaks's root with port 8080, like: http://127.0.0.1:8080. Submit the configuration to access gitlab and initialize webhook for gitlab's projects. Default webhook(External Url) is the '$base_url/web_hook/' like http://127.0.0.1:8080/web_hook/. If your gitlab's version is higher than 10.6, remember to check the option ["Allow requests to the local network from hooks and services"](https://docs.gitlab.com/ee/security/webhooks.html) in the "Outbound requests" section inside the Admin area under Settings. 
* Step 2: In the addhook page, choose the projects that you would like to add the webhook.
* Step 3: If you would like to bind the webhook to your new project automatically, just configure the system hook '$base_url/system_hook' to your gitlab， like: http:/127.0.0.1:8080/system_hook/.

# Reference
* [Install Docker-Compose](https://docs.docker.com/compose/install/)
* [Initializing Grafana with preconfigured dashboards](https://ops.tips/blog/initialize-grafana-with-preconfigured-dashboards/)
* [Dockerize Simple Flask App](http://containertutorials.com/docker-compose/flask-simple-app.html)
* https://hub.docker.com/_/mariadb/
* https://hub.docker.com/r/grafana/grafana/
* [Using MySQL in Grafana - Configure the Datasource with Provisioning](http://docs.grafana.org/features/datasources/mysql/#configure-the-datasource-with-provisioning)
* [Provisioning Grafana](http://docs.grafana.org/administration/provisioning/)
* [Webhook for gitlab's events](http://developer.dpstorm.com/help/user/project/integrations/webhooks.md)
* [System hook for gitlab's events](https://docs.gitlab.com/ee/system_hooks/system_hooks.html)
* [Python-gitlab](http://python-gitlab.readthedocs.io/en/stable)
