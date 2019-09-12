
### - 代码如下：

```
from collections import Counter


def nr(str):
    dictCount = Counter(str)  # 第一步计数
    listSort = sorted(dictCount.items(), key=lambda d: d[1], reverse=True)  # 第二步排序
    dictSout = dict(listSort)  # 第三步
    listNr = []
    listNP = []
    dictSoutKey2 = sum(list(dictSout.values()), list(dictSout.values())[1]) - list(dictSout.values())[0]

    for j in range(list(dictSout.values())[0]):
        for i in range(dictSout.__len__()):
            if list(dictSout.values())[i] > 0:
                if sum(list(dictSout.values())[1:]) == 0 and list(dictSout.keys())[i] is listNr[dictSoutKey2 - 1]:
                    count = 1
                    for k in range(listNr.__len__() - 1):
                        if list(dictSout.keys())[i] is listNr[k] or list(dictSout.keys())[i] is listNr[k + 1]:
                            count += 1
                            if count >= listNr.__len__():
                                listNP += list(dictSout.keys())[i]
                                break
                        else:
                            # listNr[k:k + 1] = list(dictSout.keys())[i]
                            listNr.insert(k + 1, list(dictSout.keys())[i])
                            break
                else:
                    listNr += list(dictSout.keys())[i]
                    dictSout[list(dictSout.keys())[i]] = list(dictSout.values())[i] - 1
                if listNr.__len__() - 1 >= dictSoutKey2:
                    dictSoutKey2 += 1

            else:
                listNr += ''

    print("原序列 \n", str)
    print("最优可排序列\n", listNr)
    print("存在不可重排序列元素：", listNP)



if __name__ == '__main__':
    s = ['a', 'a', 'a', 'a', 'a', 'a', 'a', 'a', 'a', 'a', 'a', 'a', 'a', 'a', 'a', 'a', 'b', 'c', 'b', 'c', 'b', 'c', 'b', 'c', 'a', 'a', 'a', 'a', 'b', 'c', 'b', 'c', 'b', 'c',
         'b', 'c']
    nr(s)

```

### - 算法思路

假设原序列为S1
1. 对S1计数，得到dict类型序列S2
2. 对S2排序，得到list类型序列S3
3. S3转型dict，得S4
4. 对S4重排，直至values值最大的key剩下，得S5

```
{'a':3,'b':1} -> ['a','b'] 
{'a':2,'b':0},a剩下
```

5. 将S4中剩余元素通过比较插入到S5中

```
{'a':2,'b':0} + ['a','b'] -> ['a','b','a']
{'a':1,'b':0},a剩下,不可重排
```

6. 返回最优可排序列


### 效果

![image](http://prt4c38a0.bkt.clouddn.com/Nr.PNG)