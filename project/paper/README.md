---
bibliography: references.bib
---
# System Design and Principles
> PanZhiQing

## 1. Principles

### 1.1. Very Long Baseline Interferometry (VLBI)
Space VLBI, SVLBI

干涉测量技术是一种通过测量两个或多个波源之间的相位差来确定波源位置的技术。若我们使用口径为 $D$ 的望远镜来观测波长为 $\lambda$ 的电磁波，那么望远镜的角分辨率可以用如下公式来估算：

$$
\theta = \frac{\lambda}{D} \tag{1}
$$

我们可以发现，望远镜的角分辨率与波长成反比，与口径成正比，即在观测的电磁波波长不变的情况下，仪器的口径越大，其角分辨越小，分辨能力越高。这也解释了用于观测无线电波的射电天文望远镜动辄几十米到几百米的口径的原因。同时，假设我们选择波长较短的电磁波作为观测对象，例如X射线、伽马射线等，那么我们就可以使用相对较小的望远镜口径实现较高的角分辨率，这也是采用X射线来观测脉冲星（Pulsar）的原因。但是，X射线在大气中传播时会遭遇严重的衰减，甚至可以认为大气层对于宇宙空间发射的X射线是不透明的，因此我们只能在大气层以外的空间中观测X射线辐射，这也是空间天文卫星被用于X射线天文学的原因。


## References
<!-- https://img.chinamaxx.net/n/abroad/hwbook/chinamaxx/12566406/deea0891b3014d84a15189f8e64e6f2d/f6a15dc78cb62d7aa8c7e7a4e4c2dc99.shtml?tp=jpabroad&fenlei=14020409&spage=1&username=158.132.13.163 -->
<!-- pandoc README.md --citeproc --csl=apa.csl -o output.docx -->

<!-- https://www.bruot.org/ris2bib/ -->

<!-- https://imagine.gsfc.nasa.gov/science/toolbox/emspectrum1.html -->

