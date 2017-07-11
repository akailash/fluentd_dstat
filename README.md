# fluentd_dstat
Use dstat(docker) and fluentd(docker) to monitor system

Currently uses infoslack/dstat as input and a fluentd regex filter to parse the dstat output. The data is saved in elasticsearch and sent to kibana.

## How to use
To clone this repository and run the docker-compose use the following commands

    git clone https://github.com/akailash/fluentd_dstat.git
    docker-compose up

This will spawn 4 docker containers locally:

    infoslack/dstat 
        - Runs dstat command with the option "-tcm 5" collecting cpu and memory metrics every 5 seconds to fluentd logging driver)
    fluentd
        - Builds and runs fluentd Dockerfile in ./fluentd/Dockerfile with the fluentd conf file ./fluentd/conf/fluent.conf
    elasticsearch
    kibana

If you want to change the dstat options to get a different output, please be sure to make corresponding changes to the regex filter in the fluentd conf file to parse the new output.

## Note:
To connect to RabbitMQ server remotely, do not use the guest/guest login/passwd that is created by default. Make a new user with the following commands:

    sudo rabbitmqctl add_user test test
    sudo rabbitmqctl set_user_tags test administrator
    sudo rabbitmqctl set_permissions -p / test ".*" ".*" ".*"

Also note that the elasticsearch and kibana containers have not been configured to limit memory usage. resource_limits should be set in the docker-compose as well as the corresponding env options if intending to use it for long periods of time.
