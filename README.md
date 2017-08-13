#My stupid boss#
CentOS7安装SS
安装 pip
pip是 python 的包管理工具。在本文中将使用 python 版本的 shadowsocks，此版本的 shadowsocks 已发布到 pip 上，因此我们需要通过 pip 命令来安装。
在控制台执行以下命令安装 pip：
$ curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
$ python get-pip.py
安装完成后，需要创建配置文件/etc/shadowsocks.json，内容如下：
{
  "server": "0.0.0.0",
  "server_port": 8388,
  "password": "uzon57jd0v869t7w",
  "method": "chacha20"
}
配置自启动
新建启动脚本文件/etc/systemd/system/shadowsocks.service，内容如下：

[Unit]
Description=Shadowsocks

[Service]
TimeoutStartSec=0
ExecStart=/usr/bin/ssserver -c /etc/shadowsocks.json

[Install]
WantedBy=multi-user.target

执行以下命令启动 shadowsocks 服务：

$ systemctl enable shadowsocks
$ systemctl start shadowsocks
为了检查 shadowsocks 服务是否已成功启动，可以执行以下命令查看服务的状态：

$ systemctl status shadowsocks -l
