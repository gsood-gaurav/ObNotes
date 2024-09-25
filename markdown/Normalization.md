> Instance Norm: $n*c*w*h->wh*cn$, then we do mean on $wh$. For each channel $(c)$ and each example $(n)$, we minus it with corresponding mean. 
> Group Norm: $n*c*w*h->swh*gn$ where $sg=c$. For each group $g$ and for 
> each example $n$ we minus it with corresponding mean
> Batch Norm: $n*c*w*h-> nwh*c$ then we do mean on $nwh$. For each channel $c$ we minus it with corresponding mean which is calculated for whole batch of pixels.
> Layer Norm: $n*c*w*h->cwh*n$ For each example we take mean of all pixels calculated over all channels and pixels.


 