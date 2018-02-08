[Top](https://github.com/kemixkoo/docker-docs)

### Oh, Shit 
- Oh, shit, Dockerfile里的卷(Volume)
  问题重现，当用[jenkins](https://hub.docker.com/r/kemixkoo/jenkins-maven/) image时，由于JENKINS_HOME在Dockerfile中被设置成Volume，将导致如下一些问题：
   1. USER受限，尽管在Dockerfile里指定了USER是jenkins，COPY操作后的文件，在生成的image里居然是root用户跟组，而不是想要的jenkins。
   2. RUN命令通过root用户或者sudo方式受限，即便是在Dockerfile里，运行chown跟chmod命令修改权限，都最终不会有任何效果，仍旧保持root权限。
   3. Commit受限，如果采用docker commit方式，先在容器内修改权限，然后commit，如果是volume的目录，任何修改都不将保持并被提交。
   结论：volume内的文件权限，应该受启动容器的docker用户影响
   

