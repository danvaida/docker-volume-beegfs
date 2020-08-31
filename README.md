我是光年实验室高级招聘经理。
我在github上访问了你的开源项目，你的代码超赞。你最近有没有在看工作机会，我们在招软件开发工程师，拉钩和BOSS等招聘网站也发布了相关岗位，有公司和职位的详细信息。
我们公司在杭州，业务主要做流量增长，是很多大型互联网公司的流量顾问。公司弹性工作制，福利齐全，发展潜力大，良好的办公环境和学习氛围。
公司官网是http://www.gnlab.com,公司地址是杭州市西湖区古墩路紫金广场B座，若你感兴趣，欢迎与我联系，
电话是0571-88839161，手机号：18668131388，微信号：echo 'bGhsaGxoMTEyNAo='|base64 -D ,静待佳音。如有打扰，还请见谅，祝生活愉快工作顺利。

# docker-volume-beegfs

Docker Volume plugin to create persistent volumes in a [BeeGFS](http://www.beegfs.com/content/) cluster.

## Preconditions

- BeeGFS cluster has to be setup and running
- `beegfs-client` service needs to be running on the Docker host

## Installation

A pre-built binary as well as `rpm` and `deb` packages are available from the [releases](https://github.com/RedCoolBeans/docker-volume-beegfs/releases) page.

### RedHat/CentOS 7

An rpm can be built with:

    make rpm

Then install and start the service:

    yum localinstall docker-volume-beegfs-$VERSION.rpm
    systemctl start docker-volume-beegfs

### Debian 8

Debian packages are currently built on a RedHat system, but the `Makefile`
describes which packages to install on Debian when building from scratch.
Building the actual package can be done on a Debian system without Makefile modifications:

    make deb

Now you can install and start the service:

    dpkg -i docker-volume-beegfs_$VERSION.deb
    systemctl start docker-volume-beegfs

### Others

Build the plugin:

    go build

## Usage

First create a volume:

    docker volume create -d beegfs --name postgres-portroach

Then use the volume by passing the name (`postgres-1`):

    docker run -ti -v postgres-portroach:/var/lib/postgresql/data --volume-driver=beegfs -p 5432:5432 -e POSTGRES_PASSWORD=postgres postgres

Inspect the volume:

    docker volume inspect postgres-portroach

Remove the volume (note that this will _not_ remove the actual data):

    docker volume rm postgres-portroach

### Non-default mount points

By default BeeGFS uses `/mnt/beegfs` as the mount point (as configured in
`beegfs-mounts.conf`), and this plugin does too. For non-standard mount points
you can specify an alternate root when creating a new volume:

    docker volume create -d beegfs --name b3 -o root=/stor/b3

Other options are currently silently ignored.

## Roadmap

- No outstanding features/requests.

## License

MIT, please see the LICENSE file.

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
