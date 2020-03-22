source: Support/Performance-general.md
path: blob/master/doc/

Work in Progress

# Performance tuning in general

Performance tuning is a wide topic which boils down to the simple fact that there will always be at least one hardware bottleneck. Elliminate one hardware bottleneck, and another will eventually take its place. The goal is rarely to utilize *all* the hardware resources so they operate at max capacity, and 'go faster' is imprecise at best.

Figuring out what is your current bottleneck is really beyond the scope of LibreNMS, but this document may serve as a starting point. Contributions are welcome.

Exactly what you should tune *for* is not always obvious. In a single purpose computer it is often about maximizing the throughout or getting to the result as quickly as possible.

On a shared computer or in a virtual environment, it may often be beneficial to flatten the load as much as possible. This allows for better utilization of the available hardware, which in turn allows us to buy exactly the right size of $stuff. Or in other words: we avoid having to scale our hardware for the occasional peak in whatever resource is peaking.

But it could just as well be important to tune for predictable responsetimes, a given power envelope or whatever. Also be aware that tuning for a single metric may occasionally turn out to be a pessimization, as some other bottleneck suddenly takes precedence.

An example of this is when you change an algorithm to perform better by utilizing way more memory. Suddenly the bottleneck is no longer the CPU, but memory, or even disk because you are swapping. Occasionally, the Operating System itself may offer tuning knobs. Unsurprisingly, having *more* knobs to turn does not make the job easier. 

Sometimes, the limitations are fixed, other times they are not. Adding more memory is often feasible, other limitations may require more effort to remedy. The important thing is to understand what you are optimizing *for*, figuring out which resource(s) is your current bottleneck, and what knob(s) to turn to fix it.

Lather, rinse, repeat.

The skills required for doing this requires some time and dedication to master, which is why most end up throwing more hardware at performance problems instead. *This is a valid and highly pragmatic solution.* It may not always work out, or be an available option.

If you are not discouraged yet:

For computers, the classic bottlenecks are:
1. hardware
* CPU (cycles, clock, temperature, power)
* Network IO (bandwidth, IOPS)
* Memory (size, bandwidth)
* Cache (size, bandwidth)  applies to both Disk and CPU
* Disk (size, bandwith, IOPS)

Add in shared environments and/or resources (be it virtual machines/hardware, hypervisors or general servers doing multiple things) and the picture quickly becomes quite fuzzy. 

2. the operating system
The Operating System, offers a myriad of virtual knobs, buttons and switches and various magic incantations not to be uttered in polite company.

3. application
And finally, the application on top. In the case of LibreNMS, we are polling data via the network, writing to RRDs on disk (or to the net via NFS), and communicating with MySQL (locally, or via the net). MySQL reads and writes data to disk. 

If the hardware is a 'fixed size', it is generally accepted that you should spend the bulk of your optimization and tuning efforts on the application. 1000s of times the resources you have available have already been spent on tuning the OS. That said, specific workloads can certainly merit tuning OS parameters. 


## Tools

* librenms (the software can monitor the server it runs on, via snmp. Some configuration may be required.)
* top/htop/atop/mpstat
* iostat/iotop
* vmstat

## Resources

This is a small selection of online resources offering explanations and examples for one or more of the tools mentioned above. Contents have not been vetted or validated.

* [Linux Performance Monitoring Intro](https://www.thegeekstuff.com/2011/03/linux-performance-monitoring-intro/)
* [Performance issues - how and where to start in Linux](https://www.simplylinuxfaq.com/2017/12/performance-issues-how-and-where-to-start-in-linux.html)
* [Command line tools to monitor Linux performance](https://www.tecmint.com/command-line-tools-to-monitor-linux-performance/)
* [Disk IO analysis](https://haydenjames.io/linux-server-performance-disk-io-slowing-application/)
* [atop](https://haydenjames.io/use-atop-linux-server-performance-analysis/)

## Method

0. understand what to optimize *for*
1. observe, measure and document the performance
2. evaluate data and identify the bottleneck
3. do *one* change intended to elliminate or minimize the impact of the bottleneck. document the change.
4. go to 1.

