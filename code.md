### Python-Hz  
```
import time

time_1 = time.time()
time_2 = time.time()
time_interval = time_2 - time_1

print("{:2.3f} Hz".format(1/time_interval))
```

### C-Hz
```
#include <iostream>
#include <chrono>

int main() {
    auto t1 = std::chrono::high_resolution_clock::now();
    
    double d = 0.1;
    for (int i = 0; i < 10000000; ++i) {
      d = d * d;
    }
    auto t2 = std::chrono::high_resolution_clock::now();
    std::chrono::duration<double, std::milli> fp_ms = t2 - t1;
    std::chrono::duration<double, std::micro> fp_us = t2 - t1;
    
    std::cout << "for took " << fp_ms.count() << " ms" << std::endl;
    std::cout << "for took " << fp_us.count() << " us" << std::endl;
}
```

### 
```

```

### 
```

```

### 
```

```

### 
```

```

### 
```

```

### 
```

```

