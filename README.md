# distributedTaskScheduler

### Distributed Task Scheduler

#### Implementation

1. run the command `docker build -t imagename ./` at the root directory
2. run the commands `docker run -dit --name taskpool -h taskpool -v /YOUR_LOCAL_PATH/distributedTaskScheduler:/root/distributedTaskScheduler imagename`, `docker run -dit --name master -h master -v /YOUR_LOCAL_PATH/distributedTaskScheduler:/root/distributedTaskScheduler imagename`, `docker run -dit --name slave1 -h slave1 -v /YOUR_LOCAL_PATH/distributedTaskScheduler:/root/distributedTaskScheduler imagename`, `docker run -dit --name slave2 -h slave2 -v /YOUR_LOCAL_PATH/distributedTaskScheduler:/root/distributedTaskScheduler imagename`, `docker run -dit --name slave3 -h slave3 -v /YOUR_LOCAL_PATH/distributedTaskScheduler:/root/distributedTaskScheduler imagename`
3. run mongodb service at localhost
4. make sure the container can find each other by whatever way you want to use (manually set in /etc/hosts, docker bridge)
5. start the taskpool `./scheduler/taskpool.py` for inserting 100 tasks
6. start the master `./scheduler/master.py`
7. start the slaves with hostname and the master host:

```
./scheduler/slave.py slave1 5000 master:5000
./scheduler/slave.py slave2 5000 master:5000
./scheduler/slave.py slave3 5000 master:5000
```

7. Use Ctrl-C to kill master or slave. The killed tasks should attach to the log file.
