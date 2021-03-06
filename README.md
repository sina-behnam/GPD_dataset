# GPD Dataset
__Gastric Precancerous Diseases__ classification
using __YOLOv5__ with `yolov5x` model.
## Dataset description
This dataset has _three_ classes which splited into **train**, **test**, and **validation** subsets. 

It is described in tabel below.

|dataset   |   Erosion |   Polyp |   Ulcer |
|:-----|:---------:|:-------:|:-------:|
|train |       889 |     868 |     891 |
|test  |       176 |     189 |     186 |
|valid |       144 |     159 |     165 |
|`std` |   421.192 | 400.962 | 413.228 |

You can find the acualle images with their corresponding labels under each subset directory.

Notice:
>In this case, the bounding box has drawn over the whole image.

## Inferences
This directory contain all output images and their corresponding labels, that has been detected by `yolov5x` model.

In Code snippet below show how to calculate accuracy over object detection by their confidence.
```python
import glob

classes = {
    0 : 'Erosion',
    1 : 'Polyp',
    2 : 'Ulcer'
}
Accurate = 0
Inaccurate = 0
for label in glob.glob('inference/labels/*.txt'):

    class_name = label.split('\\')[1].split('.')[0].split('_')[0]
    
    conf = []
    with open(label) as f:
        for line in f.readlines():
            c = int(line.split(' ')[0])
            t = (float(line.split(' ')[-1].split('\n')[0]),c)
            conf.append(t)

    conf.sort(reverse=True)

    if classes[conf[0][1]] == class_name:
        Accurate += 1
    else:
        Inaccurate += 1

print('The Number of Accurate detection : ', Accurate)

print('The Number of Inaccurate detection : ', Inaccurate)

print('Accuracy precentage : ',round((Accurate/(Accurate+Inaccurate))*100),3)
```
The output results 

|   Accurate | Inaccurate | Accuracy |
|:---------:|:-------:|:-------:|
|      523 |     24 |     `95.612 %` |

### Cantact information 
For further information .

gmail : sina.behnam.ai@gmail.com