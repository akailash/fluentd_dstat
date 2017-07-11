# fluentd_dstat
Use dstat(docker) and fluentd(docker) to monitor system

Currently uses infoslack/dstat as input and a fluentd regex filter to parse the dstat output. The data is saved in elasticsearch and sent to kibana.

WIP:
Intend to add support to pipe data to rabbitmq server and update dockerfile and compose to allow environment variables to select data output parameters


## Note:
To connect to RabbitMQ server remotely, do not use the guest/guest login/passwd that is created by default. Make a new user with the following commands:

    sudo rabbitmqctl add_user test test
    sudo rabbitmqctl set_user_tags test administrator
    sudo rabbitmqctl set_permissions -p / test ".*" ".*" ".*"


