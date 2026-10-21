# Hardware Overview


<iframe src="../../viewer1.html" width="100%" height="460" frameborder="0"></iframe>


## Board Layout

![Block diagram](../images/board-layout-demo.png){ width="400" .center}

- Status: On working...

## Block Diagram

<!-- TODO: insert block diagram image -->
![Block diagram](../images/block-diagram.png)

## LTE Modules Tested

The iChidori-Crest has been tested with the following LTE modules:

| LTE Module    | Category          | Interface  |
|---------------|-------------------|------------|
| Quectel EC21-J | LTE Cat 1        | USB + UART |
| Quectel BG96   | LTE Cat M1 / NB-IoT | USB + UART |

Other LTE modules should be work, provided they use a compatible mPCIe form factor and interface configuration.

!!! note
    The mPCIe LTE I²C interface is not connected in the current board revision. Use USB or UART for LTE communication.

