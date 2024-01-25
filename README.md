## 第一拍

![Untitled]([https://prod-files-secure.s3.us-west-2.amazonaws.com/e986544c-e205-431e-a304-1609de685016/f4e4338a-ec85-421b-9040-3ab8c8c98b38/Untitled.png](https://www.notion.so/coolljq/8350a9c2ee5e404bac571b19e870063e?pvs=4#f1189f0c892740b69087019eb7756816))

根据输入的header的有效位数为2，即0111，后三个字节有效，根据数据拼接

header数据为00000038，发方data_in数据从00001fe0开始递增

收方接收到的 将是(用不同颜色区分不同data)

`000038`00  001fe000  001fe100  001fe200…

收方的ready_out 设置为随机无效

可见第一次收方握手接收信号为 `000038`00，其中000038为有效header，00为data

无气泡传输

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e986544c-e205-431e-a304-1609de685016/66f004d8-f250-483c-bcca-e900f147d0ec/Untitled.png)

图示时刻接收方拉低ready_out

## 最后一拍

根据输入的header的有效位数为0111，即后三个字节有效，根据数据拼接

如header数据为00000038，data_in数据从00001fe0开始递增

收方接收到的 将是(用不同颜色区分不同data)

`000038`00  001fe000  001fe100  001fe200…

发送方的最后一个数据为00002050，其到来时last_in有效，并且keep_in为1110，即前三个字节为有效数据，根据逻辑，最后一个输出数据应该是00200000(最后四个零为无效数据)

根据仿真结果：

由于

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e986544c-e205-431e-a304-1609de685016/c4a958f5-dc4e-4532-9b40-b8526c744d3d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e986544c-e205-431e-a304-1609de685016/c1d7b7c4-2dd2-452f-84bf-18e32add9277/Untitled.png)
