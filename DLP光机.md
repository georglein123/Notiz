DLP光机

- 紫外光波段：紫外光又可细分，主要利用UVA波段，波长较长波段，385-405，对人体无害，

- 光机组成：

![image-20220617101341206](E:\文档\GitHub\Notiz\DLP光机.assets\image-20220617101341206.png)

- 工作原理：
- DMD

A DMD chip has on its surface several hundred thousand microscopic mirrors arranged in a rectangular [array](https://en.wikipedia.org/wiki/Array_data_structure) which correspond to the pixels in the image to be displayed. The mirrors can be individually rotated ±10-12°, to an on or off state. In the on state, light from the projector bulb is reflected into the lens making the pixel appear bright on the screen. In the off state, the light is directed elsewhere (usually onto a [heatsink](https://en.wikipedia.org/wiki/Heatsink)), making the pixel appear dark. To produce [greyscales](https://en.wikipedia.org/wiki/Greyscale), the mirror is toggled on and off very quickly, and the ratio of on time to off time determines the shade produced (binary [pulse-width modulation](https://en.wikipedia.org/wiki/Pulse-width_modulation)).[[4\]](https://en.wikipedia.org/wiki/Digital_micromirror_device#cite_note-Brennesholtz-4) Contemporary DMD chips can produce up to 1024 shades of gray (10 bits).[[5\]](https://en.wikipedia.org/wiki/Digital_micromirror_device#cite_note-5) See [Digital Light Processing](https://en.wikipedia.org/wiki/Digital_Light_Processing) for discussion of how color images are produced in DMD-based systems.

工艺相关：

- 均匀性校准：调节灰度，改变的灰度值会记录在上位机文件中，软件会调用该文件作用在DMD上，值越小，DMD偏转角度越大，将光偏转到周围，从而投出来的光强变暗，
- 光强校准：光度计放在料盘中间，按照已经有的光强和电流关系，去调节电流，从而整体拉高







固定波段紫外光+树脂反应，反应会发热

哪些过程会对光路有影响：

- 光机整体结构

- 保护玻璃：玻璃对光路的影响

- 料盘：

- 外界物质干扰如灰尘