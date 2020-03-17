source: Support/Performance-general.md
path: blob/master/doc/

# Performance tuning in general

Performance tuning is wide topic which boils down to the simple fact that there will always be at least one hardware bottleneck. Elliminate one hardware bottleneck, and another will eventually take it's place. The goal is rarely to utilize all the hardware resources so they operate at max capacity. 

But exactly what you should tune for is not always obvious. In a single purpose computer it is often about maximizing the throughout or getting to the result as quickly as possible.

On a shared computer or in a virtual environment, it may often be beneficial to flatten the load as much as possible. This allows for better utilization of the available hardware.

But it could just as well be important to tune for predictable responsetimes, a power envelope or whatever. Also be aware that tuning for a single metric may occasionally be a pessimization, as some other bottleneck suddenly takes precedence.

An example of this is when you change an algorithm to perform better by utilizing way more memory. Suddenly the bottleneck is no longer the CPU, but memory, or even disk because you are swapping.  

For computers, the classic *hardware* bottlenecks are:
CPU (cycles, clock, temperature, power)
Network IO (bandwidth, IOPS)
Memory (size, bandwidth)
Cache (size, bandwidth)  applies to both Disk and CPU
Disk (size, bandwith, IOPS)

Figuring out what is your current bottleneck is beyond the scope of this document or Librenms, but contributions are welcome.

As a minimum, you should be familiar with top/htop.

