# List of Commands

## Setting up packages

### Rebuilding package
```bash
colcon build
source install/setup.bash
```



## Nodes
### Checking nodes
```bash
ros2 pkg executables <your_pkg>
```

### Running node
```bash
ros2 run <your_pkg> <node>.py
```