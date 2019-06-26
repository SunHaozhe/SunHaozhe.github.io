---
title: Python multiprocessing gather
description: >
  Python skills
---

```
import multiprocessing, os
import numpy as np

def worker(seed):
	print("begin worker", seed)
	res = seed * 2
	print("end worker", seed)
	return res, res - 1

nb_processes = 16

print("There are %d CPUs, we run %d experiments in parallel." % (os.cpu_count(), nb_processes))

pool = multiprocessing.Pool(processes=nb_processes)

random_seeds = [10 * i for i in range(1, nb_processes + 1)]

array1 = np.zeros(nb_processes)
array2 = np.zeros(nb_processes)

for i, seed in enumerate(random_seeds):
	array1[i], array2[i] = pool.apply_async(worker, (seed,)).get()

print('Waiting for all subprocesses done...')
pool.close()
pool.join()

print('All subprocesses done.')

print(array1)
print(array2)
```

The output is 
```
There are 8 CPUs, we run 16 experiments in parallel.
begin worker 10
end worker 10
begin worker 20
end worker 20
begin worker 30
end worker 30
begin worker 40
end worker 40
begin worker 50
end worker 50
begin worker 60
end worker 60
begin worker 70
end worker 70
begin worker 80
end worker 80
begin worker 90
end worker 90
begin worker 100
end worker 100
begin worker 110
end worker 110
begin worker 120
end worker 120
begin worker 130
end worker 130
begin worker 140
end worker 140
begin worker 150
end worker 150
begin worker 160
end worker 160
Waiting for all subprocesses done...
All subprocesses done.
[ 20.  40.  60.  80. 100. 120. 140. 160. 180. 200. 220. 240. 260. 280.
 300. 320.]
[ 19.  39.  59.  79.  99. 119. 139. 159. 179. 199. 219. 239. 259. 279.
 299. 319.]
```

This experiment was run on Linux-4.9.125-linuxkit-x86_64-with-Ubuntu-18.04-bionic (indeed, in a docker Virtual Machine).
