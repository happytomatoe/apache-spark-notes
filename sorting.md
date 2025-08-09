From this [stackoverflow](https://stackoverflow.com/questions/32887595/how-does-spark-achieve-sort-order) thread:

Sorting in Spark is a multiphase process which requires shuffling:
- input RDD is sampled and this sample is used to compute boundaries for each output partition (sample followed by collect)
- input RDD is partitioned using rangePartitioner with boundaries computed in the first step (partitionBy)
- each partition from the second step is sorted locally (mapPartitions)


So underneath the covers orderBy uses [RangePartitioner](https://github.com/apache/spark/blob/ccff9980762fd83f2619532028c04cb030b632bb/core/src/main/scala/org/apache/spark/Partitioner.scala#L176)

There are also different methods on how to sorting in spark:
- Global sorting
scala
.orderBy()
'''

f//local only sorting
.sortWithinPartitions
'''

