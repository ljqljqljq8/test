# 第一拍

![image](https://github.com/ljqljqljq8/test/assets/118333395/446bc026-8931-45b6-8adf-22e1f467ae44)

根据输入的header的有效位数为2，即0111，后三个字节有效，根据数据拼接，去除无效字节

header数据为00000038，发方data_in数据从00001fe0开始递增

收方接收到的 将是(用不同颜色区分不同data)

`000038`00  001fe000  001fe100  001fe200…

收方的ready_out 设置为随机无效，根据仿真结果：

可见第一次收方握手接收信号为 `000038`00，其中000038为有效header，00为data

# 最后一拍

![image](https://github.com/ljqljqljq8/test/assets/118333395/3ffd6675-49ef-4137-8abf-b30d899a9971)

发送方的最后一个数据为`0000202d`，其到来时last_in有效，并且keep_in为1110，即前三个字节为有效数据，根据逻辑，最后一个输出数据应该是00200000(最后四个零为无效数据)

根据仿真结果：

可见data_out为 `00200000`，并且输出端有效握手，last_out 有效，keep_out为c(1100)

# 无气泡传输 & 逐级反压

![image](https://github.com/ljqljqljq8/test/assets/118333395/e73efaf3-fb8c-477f-9a4a-c405ce6c42fd)

图示时刻接收方拉低ready_out,发送方仍然能够接收数据，并在后续有效被接收方读取

发送方的ready_in 较 ready_out 落后一拍拉低，告知发送方收方接受无力

# 无数据丢失 & 重复

![image](https://github.com/ljqljqljq8/test/assets/118333395/a6c30171-7b5c-4bab-921f-64539cedb3da)

根据仿真结果：

发送方的每一个有效valid_in下传输的数据均从data_out输出，在接收方有效握手之后接收

一次循环中，可见收方完整接收并且无重复数据

```markdown
Data is: 00003800【第一个数据，header为000038】
Data is: 001fe000
Data is: 001fe100
Data is: 001fe200
Data is: 001fe300
Data is: 001fe400
Data is: 001fe500
Data is: 001fe600
Data is: 001fe700
Data is: 001fe800
Data is: 001fe900
Data is: 001fea00
Data is: 001feb00
Data is: 001fec00
Data is: 001fed00
Data is: 001fee00
Data is: 001fef00
Data is: 001ff000
Data is: 001ff100
Data is: 001ff200
Data is: 001ff300
Data is: 001ff400
Data is: 001ff500
Data is: 001ff600
Data is: 001ff700
Data is: 001ff800
Data is: 001ff900
Data is: 001ffa00
Data is: 001ffb00
Data is: 001ffc00
Data is: 001ffd00
Data is: 001ffe00
Data is: 001fff00
Data is: 00200000
Data is: 00200100
Data is: 00200200
Data is: 00200300
Data is: 00200400
Data is: 00200500
Data is: 00200600
Data is: 00200700
Data is: 00200800
Data is: 00200900
Data is: 00200a00
Data is: 00200b00
Data is: 00200c00
Data is: 00200d00
Data is: 00200e00
Data is: 00200f00
Data is: 00201000
Data is: 00201100
Data is: 00201200
Data is: 00201300
Data is: 00201400
Data is: 00201500
Data is: 00201600
Data is: 00201700
Data is: 00201800
Data is: 00201900
Data is: 00201a00
Data is: 00201b00
Data is: 00201c00
Data is: 00201d00
Data is: 00201e00
Data is: 00201f00
Data is: 00202000
Data is: 00202100
Data is: 00202200
Data is: 00202300
Data is: 00202400
Data is: 00202500
Data is: 00202600
Data is: 00202700
Data is: 00202800
Data is: 00202900
Data is: 00202a00
Data is: 00202b00
Data is: 00202c00
Data is: 00200000【最后一个数据，后两个字节无效】
```
```markdown
当使用DATA_WD=16，byte_insert_cnt=1(两个字节均有效)，最后一个数据的keep_in=2'b10(第一位有效)
接收数据为：
Data is: 0038【第一个数据，header为0038】
Data is: 1fe0
Data is: 1fe1
Data is: 1fe2
Data is: 1fe3
Data is: 1fe4
Data is: 1fe5
Data is: 1fe6
Data is: 1fe7
Data is: 1fe8
Data is: 1fe9
Data is: 1fea
Data is: 1feb
Data is: 1fec
Data is: 1fed
Data is: 1fee
Data is: 1fef
Data is: 1ff0
Data is: 1ff1
Data is: 1ff2
Data is: 1ff3
Data is: 1ff4
Data is: 1ff5
Data is: 1ff6
Data is: 1ff7
Data is: 1ff8
Data is: 1ff9
Data is: 1ffa
Data is: 1ffb
Data is: 1ffc
Data is: 1ffd
Data is: 1ffe
Data is: 1fff
Data is: 2000
Data is: 2001
Data is: 2002
Data is: 2003
Data is: 2004
Data is: 2005
Data is: 2006
Data is: 2007
Data is: 2008
Data is: 2009
Data is: 200a
Data is: 200b
Data is: 200c
Data is: 200d
Data is: 200e
Data is: 200f
Data is: 2010
Data is: 2011
Data is: 2012
Data is: 2013
Data is: 2014
Data is: 2015
Data is: 2016
Data is: 2017
Data is: 2018
Data is: 2019
Data is: 201a
Data is: 201b
Data is: 201c
Data is: 201d
Data is: 201e
Data is: 201f
Data is: 2020
Data is: 2021
Data is: 2022
Data is: 2023
Data is: 2024
Data is: 2025
Data is: 2026
Data is: 2027
Data is: 2028
Data is: 2029
Data is: 202a
Data is: 202b
Data is: 202c
Data is: 2000【最后一个数据，第二个字节无效】

```

