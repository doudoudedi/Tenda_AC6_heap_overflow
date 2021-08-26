# Route_ Heap overflow

##### Describe

​	I found some vulnerabilities in Tenda AC6. The firmware version is  _ US_ AC6V1.0BR_ V15.03.05.16_ multi_ Td01.bin, which may cause a denial of service 

##### Details

​	https saveParentControlInfo fuction in IDA view

<img src="./Tenda/image-20210826114251359.png" alt="image-20210826114251359" style="zoom:50%;" />



​	The deviceid we entered is directly copied to the PTR heap memory through the strcpy function. The maximum size we can enter should be 0x400 bytes, but the malloc function only applied for 0x254 bytes, resulting in heap overflow

​	So we first create a new device under the home control module, and then use burpsuit to capture packets

​	Then modify the deviceid to overflow the heap and crash the program

<img src="./Tenda/image-20210826120446468.png" alt="image-20210826120446468" style="zoom:50%;" />

You can see that httpd crashed

<img src="./Tenda/image-20210826120822098.png" alt="image-20210826120822098" style="zoom:50%;" />

