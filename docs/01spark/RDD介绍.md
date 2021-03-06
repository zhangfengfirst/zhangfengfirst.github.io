# RDD特点
- RDDs执行两种类型的操作：转换算子从前一个RDD生成新的数据集，行动算子在对数据集执行计算后将值返回给driver程序。

# spark-partition and hdfs-block
- hdfs-blocks的大小是固定的；spark-partition的大小是不固定的，是大型分布式数据集的逻辑上划分的块。默认情况下，将为每个hdfs-block创建一个spark-partition。

如果在HDFS存储了30GB的未压缩文本文件，默认的HDFS块大小设置是128MB，数据将存储在235个块中（30*1000/128）。

# spark-partition属性

- size
- number
- partitioning scheme
- node distribution
- repartitioning

RDD在没有程序员干预的情况下是自动分区的。但是，有时候可根据应用程序调整分区的大小、数量、方案。
通常，较小/更多的分区（size小、number多）可以将工作分配给更多的worker，但是较大/更少的分区（size大、number小）可以使工作以更大的块完成，只要所有worker都保持忙碌。由于减少了开销，这可能使工作更快的完成。

增加分区的数量将使每个分区的数据更少。

分区的最大大小（size）受限于executor可用内存。