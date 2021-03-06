# pmark
python benchmarking utility

#### Requirements  
1. **OS:** macOS Maverics+ or Ubuntu 14.04+  
2. **Python:** v3.6.0+ 
3. **Tensorflow:** v1.4.0+ 


#### What is pmark?
Pmark - "Python Benchmark" is a simple yet intutive process monitoring tool, which can monitor,
1. CPU Usage
2. RAM Usage
3. GPU Usage (Supports only NVidia for now)

#### Architecture:
![Architecture](https://github.com/kingspp/pmark/blob/master/pmark.png)

1. A function with required arguments is sent to the utility.
2. The function is sent as a target for a python Process, which shares statistics using a BaseManager. 
3. Required Monitors (CPU/GPU/RAM) are attached to the current process as threads.
4. The attached monitors are given the main process `pid` which helps us in extracting consumption of resources by the process,
thereby increasing the accuracy of monitoring process.
5. Each of the monitors supports interval configuration which can be overridden by benchmark interval.
6. The threads for each monitor continues to run, untill main process is completed, once done, all the threads,
including the main process are closed. 


#### Installation
```bash
python3 -m pip install pmark
```

#### Usage


1. Basic Usage
```python
from pmark import pmonitor
import time

# Declare function and its body
@pmonitor
def random_function():
    time.sleep(5)
    x = [i**2 for i in range(1000)]
    time.sleep(5)

# Call the function
random_function()
    

```

2. Monitor Time
```python
from pmark import ftimer
import time

# Declare function and its body
@ftimer
def random_function():
    time.sleep(5)
    x = [i**2 for i in range(1000)]
    time.sleep(5)

# Call the function
random_function()
```

3. Monitor Memory
```python
from pmark import fmemory

# Declare function and its body
@fmemory
def random_function():
    import time
    time.sleep(5)
    x = [i**2 for i in range(1000)]
    time.sleep(5)

# Call the function
random_function()
```