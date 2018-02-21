# Transactional GPU Kernel Scheme

This preemptive GPU scheduler for ARM Mali-T628 GPU is an OS-level solution to the priority inversion problem. Exploiting the shared physical memory between the CPU and GPU in heterogeneous system architecture (HSA), we propose an approach to transactionize the GPU kernels. By snapshotting the kernel GPU memory in advance, A transactionized GPU kernel can be aborted at any point during its execution and rolled back to its initial state for re-execution. Based on this transactionizing GPU kernels, it is possible to evict low-priority kernels and immediately schedule high-priority kernels forcibly. The preempted low-priority kernel instances can be re-executed after a GPU becomes available.

Our preemptive GPU scheduling concept is implemented in the device driver of a Mali T-628 MP6 GPU based on a Samsung Exynos 5422 system on chip (SoC). To apply our implementation to the Exynos 5422 system, you must install a specific kernel version 3.10.72 because our code is currently supporting that specific version. You can download the kernel 3.10.72 for Exynos from Hardkernel Github repository (https://github.com/hardkernel/linux). In order to apply our schemes to the Linux kernel, patch the downloaded original Mali driver with our Mali GPU device driver patch file.

## How to patch and build
To apply our customizing GPU device driver to original kernel, you should download a patch file on your kernel source directory and patch to kernel following this.

	[kernel dir]$ sudo patch -p1 < [patch file]

To build and install patched kernel,

	[patched kernel dir]$ sudo ./install.sh

## How to use our preemptive GPU scheduler
To use our preemptive GPU scheduler, you only designate priority(NICE value) of each of applications by 'nice' command when running a GPGPU program. Especially, if you apply NICE value '-20' to a task, this task will run with the highest priority without snapshot process. For example,
	
	$ nice -n -20 [task]
	
## Note that
Our preemptive GPU scheduler map the GPU memory region and snapshot memory to kernel virtual memory space through vamp function. This is a fast way to quickly map physical memory page to contiguous virtual memory, but, kernel virtual memory space can be insufficient in 32-bit architecture. This problem can be mitigated by increasing kernel virtual memory space size. Sure, this spatial problem will not occur in 64-bit architecture with very large virtual memory space.

	
