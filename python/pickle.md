```python
import pickle

d = dict(name = '思聪', age = 29, score = 80)

#序列化
str = pickle.dumps(d)

#序列化并存入本地文件中
with open('dupm.txt', 'wb') as f:
    pickle.dump(d, f)

#从内存中进行反序列化
pickle.loads(str)

#从本地文件中进行反序列化
with open('dupm.txt', 'rb') as f:
    d = pickle.load(f)
```