# Basic Java IO Notes

The general concept is similar in other language as well. There are three layers for the read IO operations. On the first layer, we choose the format of stored data either as text data or binary data. On the second layer, we want to avoid excessive disk IO access, so we use in memory buffer to avoid flushing or reading from disk too often. On the third layer, we want to facilitate data processing, converting strings, integers or objects to binary data or parse binary data to get back strings, integers or objects.

## Tow types of IO

* Un-buffered IO: Each read or write request is handled directly by the underlying OS
* Buffered IO: **It maintains a in-memory buffer**. The native input API is called only when the buffer is empty, and the native output API is called only when the buffer is full.

## Buffered Streams

There are four different buffered stream classed used to wrap un-buffered streams.

* For byte streams
  * BufferedInputStream
  * BufferedOutputStream
* For character streams
  * BufferedReader
  * BufferedWriter

## Byte Streams

* File based
  * FileInputStream
  * FileOutputStream

## Character Steams

* File based
  * FileReader
  * FileWriter

Due to historical reasons, standard streams are byte streams not character streams. A special stream for standard input stream. 

```java
InputStreamReader cin = new InputStreamReader(System.in);
```

## Scanner

```java
import java.util.Scanner
Scanner s = new Scanner(new BufferedReader(new FileReader("temp")))
s.useDelimiter(",\\s*"); // the default is white space
s.hasNext()
s.hasNextBoolean()
```

## Data Streams

If the input stream is a byte stream, wraps it with a data stream to facilitate data processing, converting text data to byte arrays and vice versa.

* DataInputStream
  * readDouble
  * readInt
  * readUTF (read strings)
* DataOutputStream
  * writeDouble
  * writeInt
  * writeUTF

## Object Streams

Data streams support I/O of primitive data. Object streams support I/O of serializable objects. 

* ObjectInputStream
  * obj = s.readObject()
* ObjectOutputStream
  * s.writeObject(obj) 