
The preemptive GPU scheduler based on ARM Mali-T628 GPU is a solution of priority inversion problem supported at operating system (OS) level. Exploiting the shared physical memory of CPUs and GPUs in heterogeneous system architecture (HSA), we propose an approach to transactionize GPU kernels. By snapshotting the kernel GPU memory in advance, A transactionized GPU kernel can be aborted at any point during its execution and rolled back to its initial state for reexecution. Based on this transactionizing GPU kernels, it is possible to forcibly evict low-priority kernels and immediately schedule high-priority kernels. The preempted low-priority kernel instances can be reexecuted after a GPU becomes available.  

Our preemptive GPU scheduling concept is implemented in the device driver of a Mali T-628 MP6 GPU based on a Samsung Exynos 5422 system on chip (SoC). For applying our implementation on your GPU system, you must use a specific kernel version 3.10.72 due to having the strong dependency of kernel implementations. You can download a kernel 3.10.72 source code on Hardkernel cooperation's Github site (https://github.com/hardkernel/linux).  Also, you can download a Mali GPU device driver path file from our Github and patch Mali GPU driver source codes to original Mali GPU driver on kernel source downloaded above.



