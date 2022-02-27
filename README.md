# PG_NestedLoopJoin_BlockedProcessing
This code is for changing the nested loop join implementation of PostgreSQL from pipeline processing to nested loop processing

For details, you might check my technical report at ZhiHu:[[PostgreSQL源码]Nested loop join源码讲解及blocked processing的实验](https://zhuanlan.zhihu.com/p/456245221)


 What I want to achieve is to collect all the return tuple from the child plan of Hash Join (specially, the Hash build node at PG's execution plan). The most modified code is at src/backend/executor/nodeHash.c, which is referenced by src/backend/utils/sort/tuplestore.c and src/backend/executor/nodeMaterial.c 
![image](https://user-images.githubusercontent.com/52020936/147085247-3b9ac023-3d4e-4b86-a58b-8a7ed0222ba5.png)

The functions that I added:
* ExecInitMaterialAtHashNode
* ExecMaterialAtHashNode
* ExecEndMaterialAtHashNode

## Usage
The code is based on PostgreSQL v13.0, you can replace the folder **src/backend/exectuor** directly, and then its supposed to work.

## Author
Fang WANG. The Hong Kong Polytechnic University 
If you are user of Wechat, you may follow my public account "LearnDB".

![qrcode_for_gh_e6d9389929b9_258](https://user-images.githubusercontent.com/52020936/147086636-6c6a5d22-b2b2-4d60-baf0-06303cbbde40.jpg)

