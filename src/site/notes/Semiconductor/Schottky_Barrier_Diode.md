---
{"dg-publish":true,"permalink":"/semiconductor/schottky-barrier-diode/"}
---

refer: [知乎视频：肖特基二极管的工作原理](https://www.zhihu.com/zvideo/1439791290892869632)，[知乎肖特基二极管](https://zhuanlan.zhihu.com/p/368078363)，[知乎肖特基二极管的基本结构与工作原理](https://zhuanlan.zhihu.com/p/471531335)

# 简介

> 肖特基二极管，又称为Schottky Barrier Diode(SBD)。金属和半导体接触的时，电子会从半导体跑到金属里面去，形成空间电荷区。这个空间电荷区，会阻止半导体的电子继续向金属移动，也就是说形成了肖特基势垒。

![400](./assets/Pasted%20image%2020220519154357.png)
![400](./assets/Schottky_Barrier_Diode.assets/Pasted%20image%2020220519163016.png)

- N失去了电子带正电，金属得到了电子带负电。
- 即形成了从N到Metal方向的自建电场，形成了势磊，阻止了电子继续从N到M。
- 当外加电压M为正，N为负时，即为正向电场时，其方向为从M到N。降低了势磊，电子即可从N流向M，形成了电流。
- 当外加电压M为负，N为正时，即为负向电场时，其方向为从N到M。增加了势磊，电流基本为0，反向偏止了。
![400](./assets/Schottky_Barrier_Diode.assets/Pasted%20image%2020220519155138.png)
# 原理
> 功函数: 也叫逸出功，就是把电子从固体内部弄到外部去，所需的最少的能量。

N型半导体的功函数小于金属的功函数，当两者接触时，即电子会从N半导体进入到Metal，形成了从N到M的自建电场，即势磊。

![400](./assets/Schottky_Barrier_Diode.assets/Pasted%20image%2020220519155217.png)
![400](./assets/Schottky_Barrier_Diode.assets/Pasted%20image%2020220519155233.png)
![400](./assets/Schottky_Barrier_Diode.assets/Pasted%20image%2020220519155249.png)
![400](./assets/Schottky_Barrier_Diode.assets/Pasted%20image%2020220519160048.png)
![400](./assets/Schottky_Barrier_Diode.assets/Pasted%20image%2020220519155309.png)
![400](./assets/Schottky_Barrier_Diode.assets/Pasted%20image%2020220519155340.png)
![400](./assets/Schottky_Barrier_Diode.assets/Pasted%20image%2020220519155405.png)
![400](./assets/Schottky_Barrier_Diode.assets/Pasted%20image%2020220519155421.png)
![400](./assets/Schottky_Barrier_Diode.assets/Pasted%20image%2020220519155444.png)
![400](./assets/Schottky_Barrier_Diode.assets/Pasted%20image%2020220519155500.png)



# 肖特基二极管和欧姆接触
实际用的PN结二极管，焊接的两个管脚是金属导体，而里面又是半导体。所以肯定有金属和半导体接触，怎么没有形成了肖特基二极管？

> 金属与半导体相接触，并不是一定会形成二极管。

- 在N型半导体掺杂很高的时候，形成的势垒会非常的薄，这时的电子，可以通过[[隧道效应?|隧道效应?]]直接就穿过这个薄的势垒了。这个势垒就相当于是一个低阻值的电阻了，没有二极管的整流特性。这种接触称为欧姆接触。

- 而掺杂低的时候，形成的势垒相对较宽，电子就不能因为隧道效应越过势垒区了，这时候会形成二极管，这种金属-半导体接触就叫肖特基接触。
![400](./assets/Schottky_Barrier_Diode.assets/Pasted%20image%2020220519160815.png)

# 肖特基二极管和普通PN二极管
和PN结相比，肖特基二极管的反向饱和电流更大，为多数载流子导通电流，具有更好的高频特性。

- 两者的正向导通压降不同: SBD的压降约为0.4V，而PN结约为0.7V。
- 肖特基二极管，它只有一种载流子，那就是电子，也是多子。
- 普通二极管的速度慢，其原因就是因为有反向恢复时间，而反向恢复时间是因为少数载流子的存储作用导致的。PN结正向导通时，由P区注入N区的空穴或由N区注入P区的电子，都是少子（所以也叫少子注入），它们先形成一定的积累，然后靠扩散运动形成电流，少子的积累使开关速度受到极大的限制。
- PN结二极管的反向漏电流是由空间电荷区电场抽取少子形成的，其大小对温度十分敏感；而肖特基二极管的反向漏电流是从金属向硅发射的电子流，由于金属中电子的密度对温度不敏感，势垒qΦM对温度的依赖性也不大，因而其值受温度变化的影响不大，但是肖特基势垒中的空间电荷区相比于PN结的要窄，在反向偏置电压的作用下，载流子的隧穿产生的电流对反向电流也有贡献，使得肖特基二极管的反向电流特性偏软。

![400](./assets/Schottky_Barrier_Diode.assets/Pasted%20image%2020220519161245.png)
![400](./assets/Schottky_Barrier_Diode.assets/Pasted%20image%2020220519155523.png)
![400](./assets/Schottky_Barrier_Diode.assets/Pasted%20image%2020220519155545.png)
