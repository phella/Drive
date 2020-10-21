# Drive
Drive project built on distributed system using python and zmq

# Description 
File storage project using distriputed systems where replicas of same file is stored to achieve avilability.

## The System Components:

### Master processes:
 - isAlive: listen to heartbeat signals from datakeepers to check they are still up.
 - events: listens to datakeepers requests to update system state.
 - tracker: listens to client requests and respond with datakeepers ips and sockets to store or restore files.
 - replica: make sure that each file is stored in more than 1 datakeeper.
 Processes communicate through shared memory.
 run Master using: 
 ```python
 python master/build.py
 ```
 
 ### Data keeper processes:
 - isAlive: send heartbeat signals to master each second.
 - Keeper: stores file in machiine file system, many threads are ran with different sockets to increase system throughput.
 - dummyclient: upload file to another datakeeper.
  run Keeper using: 
   ```python
  python keeper/build.py {id}
  ```
### Client processes:
- Client: uploads and downloads file.
run client using: 
 ```python
python client/build.py donwload/upload {filename}
```

### bully algorithm:
used to vote for a new master if current master is down

### utility:
 utiliity modules contains logging functions and array/object printing utilties
