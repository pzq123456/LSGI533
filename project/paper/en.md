---
bibliography: references.bib
---
# System Design and Principles
> PanZhiQing

## 1. Principles

### 1.1. Very Long Baseline Interferometry (VLBI)

In the case that we use a telescope with an aperture of $D$ to observe electromagnetic waves with a wavelength of $\lambda$, the angular resolution of the telescope can be estimated by the following formula:

$$
\theta^N = \frac{\lambda}{D}\rho^N \tag*{(1)}
$$

We can find that the angular resolution of the telescope is inversely proportional to the wavelength and directly proportional to the aperture, that is, when the wavelength of the electromagnetic wave being observed remains unchanged, the larger the aperture of the instrument, the smaller the angular resolution, and the higher the resolution. This also explains why radio telescopes used to observe radio waves have apertures ranging from tens of meters to hundreds of meters. At the same time, assuming that we choose shorter wavelengths of electromagnetic waves as the observation objects, such as X-rays, gamma rays, etc., we can use relatively small telescope apertures to achieve higher angular resolution, which is also the reason for using X-rays to observe pulsars. However, X-rays undergo severe attenuation when propagating in the atmosphere, and it can even be considered that the atmosphere is opaque to X-rays emitted from space, so we can only observe X-ray radiation outside the atmosphere, which is also the reason why space astronomical satellites are used in X-ray astronomy.

Interferometric measurement technology is a technique for determining the position of a source by measuring the phase difference between two or more sources. If we use two radio telescopes that are far apart to observe the same celestial body and use interferometric measurement technology to measure the phase difference of the electromagnetic waves received by the two radio telescopes, then we can measure the position of the celestial body or perform imaging through this method [@10.1093/mnras/118.3.276]. Theoretically, as long as the two radio telescopes are far enough apart, we can obtain a "virtual" telescope with excellent angular resolution. The conventional method is to use a cable to link the two telescopes for time synchronization, but the transmission process of the long cable often brings great errors, resulting in the accuracy of interferometric measurement decreasing with the increase of the baseline length.

To solve this problem, VLBI technology came into being. VLBI technology uses atomic clocks (generally hydrogen maser) to generate timestamps, and records the observation values together with the timestamps on the storage medium, and then performs data post-processing centrally. Since two atomic clocks can ensure strict time synchronization, there is no need to use cables for time synchronization.

However, this approach has at least two bottlenecks: first, the diameter of the Earth is limited, even if we set up telescopes at the North and South Poles respectively, the baseline length will not exceed the diameter of the Earth, and the theoretical highest resolution we can obtain is also limited; second, this approach lacks real-time performance, we need to wait until all data are collected before data processing can be carried out, which is unacceptable for some astronomical phenomena that require real-time observation. For the first point, some countries have proposed to deploy telescopes in space and form a VLBI observation network with ground-based radio telescopes. For the second point, real-time data processing can be achieved by leveraging modern communication infrastructure and cloud computing technology.

In 2019, people used the Event Horizon Telescope (EHT) [@Akiyama_2019] to image a black hole, which is a successful application of VLBI technology. EHT is a VLBI synchronous observation network composed of multiple radio telescope baselines around the world, and its equivalent aperture is almost equal to the diameter of the Earth.

![Figure 1: The Event Horizon Telescope](./imgs/1.png)


In summary, Very Long Baseline Interferometry can observe celestial bodies in space with extremely high resolution, providing unprecedented rich information for human beings. We can fully obtain the most accurate cosmic information database under the current technical conditions based on VLBI technology and the ultra-high-resolution cosmic observation system developed on this basis. This database records the morphology, spectrum, motion laws, and positions relative to the barycenter of the solar system (SSB) of celestial bodies in space. In the following content, we assume that this database has been loaded onto the target, and the target can read and update the database at any time.

## References
<!-- cd project/paper -->
<!-- pandoc en.md --citeproc --csl=apa.csl -o en.docx  -->

