## masked depth culling 

1. modern rasterizers typically work on tiles groups of w*h*d 

TBR tile base rendering,将屏幕分解成为一系列的瓦片tile，可以做coarse depth test,
TBR 是一种由硬件支持的渲染管线技术

2. coarse depth test
Failed,
i.e., culled, tiles are immediately thrown away and require no futher processing. Passing and ambiguous tiles are sent down the
pipeline for further processing, with the main difference being that
ambiguous tiles must be fully depth tested in the depth unit, while
trivially passing tiles can simply overwrite the contents of the depth
buffer. This is a small difference, but depending on the architecture, write-only operations may result in lower bandwidth than the
read-modify-write operation required for performing the full depth
test 