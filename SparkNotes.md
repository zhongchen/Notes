# Spark Notes

### Prerequisite
Understand which part of the code is executed on the `Spark driver` and which part of the code is excuted on the `Spark executor`

```
dstream.foreachRDD { rdd =>
  val where1 = "on the driver"
    rdd.foreach { record =>
      val where2 = "on different executors"
    }
  }
}
```

### Spark Unit Testing
* [unit testing](http://mkuthan.github.io/blog/2015/03/01/spark-unit-testing/)

### Spark and Kafka
* [part one](http://allegro.tech/2015/08/spark-kafka-integration.html)
* [part two](http://mkuthan.github.io/blog/2016/01/29/spark-kafka-integration2/)

### Online Courses