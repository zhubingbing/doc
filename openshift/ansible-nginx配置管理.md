## ansible实现nginx配置管理

### 需求分析

1. 管理上百台nginx服务器；

2. 动作：
    1. 安装 
    2. 删除 
    3. reload 
    4. 修改配置，语法检测，reload
    5. 更新

3. 实现不同要求不同组的nginx配置文件模版, 
```shell
// example 1
{% for vhost in nginx_vhosts %}
server {
listen {{ vhost.listen | default('80 default_server') }};
{% if vhost.server_name is defined %}
    server_name {{ vhost.server_name }};
{% endif %}
{% if vhost.root is defined %}
    root {{ vhost.root }};
{% endif %}
```

4. 支持nginx集群 横行扩展

5. 集群ha