## Python is Python3
```
sudo apt install python-is-python3
```

## Python-OpenCV

### - resize
```
height, width = img.shape[:2]
height_half = int(height / 2)
width_half = int(width / 2)
img_half = cv2.resize(img, (width_half, height_half), cv2.INTER_LINEAR)
```

## C++OpenCV

### - Draw
```
cv::Point: <u,v> or <col, row> pair

Vector2d uvd;
circle(img, Point(uvd[0], uvd[1]), 3, Scalar(0, 0, 255), -1);

Vec2d p1 = curr_kf.kp[index[i].first];
Vec2d p2 = frame.kp[index[i].second];
line(img, Point(p2[0], p2[1]), 
          Point(p1[0], p1[1]), Scalar(0, 255, 0));
putText(dot, "0", Point(ori.x, ori.y), FONT_HERSHEY_PLAIN,
        1,  Scalar(0,0,255), 2);

auto& t = triangle[i];
vector<Point> pts;
pts.push_back(Point(t.e1.p1.x, t.e1.p1.y));
pts.push_back(Point(t.e2.p1.x, t.e2.p1.y));
pts.push_back(Point(t.e3.p1.x, t.e3.p1.y));
fillConvexPoly(img_g, pts, COLOR_BLK);
```
### - size, rect, resize
```
size, rect, resize

Size_(_Tp _width, _Tp _height);
Rect_(_Tp _x, _Tp _y, _Tp _width, _Tp _height);

resize(img, rimg, Size(cols, rows));
resize(img, rimg, Size(), 2, 2);
```

## Python-Hz  
```
import time

time_1 = time.time()
time_2 = time.time()
time_interval = time_2 - time_1

print("{:2.3f} Hz".format(1/time_interval))
```

## Python-YYYY-MM-DD HH:MM:SS
```
import datetime
now = datetime.datetime.now()
dir_name = "{:d}".format(now.year) + \
               "-{:02d}".format(now.month) + \
               "-{:02d}".format(now.day) + \
               " {:02d}".format(now.hour) + \
               ":{:02d}".format(now.minute) + \
               ":{:02d}".format(now.second)
print( dir_name)
```

## C++Hz
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

## Python-by-name
```
#!/usr/bin/python3
chmod +x script_name.py
```

## 
```

```

