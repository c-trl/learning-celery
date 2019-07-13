1. brew install rabbitmq
2. brew link rabbitmq
3. pip install celery
4. make tasks.py:
```python
from celery import Celery

app = Celery()

@app.task
def add(x, y):
    return x + y
```
5. screen; /usr/local/sbin/rabbitmq-server
6. screen; celery worker -A tasks -l INFO
7. ipython:
```python
In [1]: from tasks import add

In [2]: for i in range(100):
   ...:     add.delay(i,i)
   ...: 
```
8. celery screen:
```bash
[2019-07-13 18:00:33,121: INFO/ForkPoolWorker-4] Task tasks.add[e0e95810-b157-4d14-bfc0-b797d1d99179] succeeded in 7.590999999251835e-05s: 19990
[2019-07-13 18:00:33,121: INFO/ForkPoolWorker-1] Task tasks.add[3bf93a42-f37e-45e0-bbb1-1fc33865ea1e] succeeded in 7.345500000610627e-05s: 19988
[2019-07-13 18:00:33,122: INFO/ForkPoolWorker-2] Task tasks.add[741b47ec-c3e1-4259-b02f-4d5ad63abf9f] succeeded in 7.577499999911197e-05s: 19994
[2019-07-13 18:00:33,124: INFO/ForkPoolWorker-1] Task tasks.add[0dc504bb-a071-44d0-8a32-0873a9b299d3] succeeded in 5.748099999891565e-05s: 19996
[2019-07-13 18:00:33,124: INFO/ForkPoolWorker-4] Task tasks.add[cbc14aeb-be33-4638-a780-6d88377ff0c8] succeeded in 7.495799999901465e-05s: 19998
...
```
