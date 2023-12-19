The "nstress" package is a set of programs to keep many parts of the computer busy including CPU, memory, file systems, inter-process communications, and disks.

Possible uses of the programs in the nstress toolbox are:
 - You can "burn in" new hardware to prove it is reliable before production use
 - You can find out how fast your computer runs like memory speeds or disk I/O
 - You can generate "fake" workloads and then use performance monitoring tools like nmon or njmon to see the performance stats in action.

If you over do the generated workload, then make sure that there is no other users on your computer (or VM) because nstress can grind your computer to a stop.

The author focuses on POWER processor-based computers but these tools are additionally compiled for AMD64 (x86_64)
​
There are a number of uses:

1. Soak testing = check a new machine/disk to remove early life failures
2. Prove performance of machine upgrades or alternative disk configurations
3. Learn performance monitoring and tuning
4. For example, I run a Performance Tuning Expert Class and need to quickly setup many different workloads and problems to be solved. 
With a 20 line shell script and these tools, I don't have to spend a week of setup time.

The programs are: 
Name	Purpose
**ncpu**	Hammers the CPUs (can be slowed down to use a percentage)
**ndisk**	Removed - use ndisk64
**ndisk64**	Hammers the disks compiled for large files so it can access large files (many GBs)
**ndiskaio**	Removed - use ndisk64
**ndiskmio**	Removed. Uses the Modular IO AIX Expansion pack library must be installed (experimental not currently available)
**nmem**	Hammers or touches memory
**nmem64**	Hammers or touches memory - complied 64 bit so it has access large memory (many GBs)
**nipc**	Tests shared memory, semaphores, and shared messages in a ring of processes - takes 1 CPU
**nlog**	Generates output like error messages. You specify the data size in kilobytes (KB) output per second
**nfile**	Creates, writes, and deletes files to push the JFS and JFS log hard
**createfs.sh**	Example script to create the file systems - you need to edit the file for your system
**dbstart.sh**	Example script to start a fake database RDBMS - you need to edit the file for your system
**webstart.sh**	Example script to start a fake web server - you need to edit the file for your system

Warnings:
Do not consider these files as benchmark programs - they are hardware stress tools.
Do not compare AIX with Linux - it is different code and different compilers. Especially ndisk64.
Do not compare Linux ppc64 and Linux x86_64 - I did not install the Advanced Tool Chain on ppc64 to get the optimized compiler, which would give up to 35% better performance.
Do not compare Linux with Linux - due to the different ages of the OS, different kernel levels, different libc, different GCC it is NOT a fair comparison. Note that some Distributions were NOT updated from current Online repositories and are the original Gold DVD level RPMs (RHEL and SLES) as I don't have repository access.
Special ndisk64 version 75 notes:
Always use the -M procs option to specify the number of processes to use or it hangs.
Recommended: using the -s size option to specify the file size
The Async I/O is completely missing in the code - don't believe the -? help.
The command-line option -C for CIO and -D for DIO are not available. 
Use Direct I/O by using the /dev/rsda9 type volume but make sure it is NOT a file system or it trashes your files in a nanosecond.
The Source Code is not available to the public.

Warranty = none
 - It is strictly at your own risk.
 - It is possible to hang the entire server.
 - Use the option that stops the tool in say 5 minutes otherwise you need to halt your server or VM the hard way.
 - If you run these programs as a regular user, then no harm can be to your system.
 - If you run these programs as the root user, they can be dangerous and even hang the machine due to total saturation of CPU or memory or disk I/O.

Warning
 - Note: ncpu when run by the root user tries to boost its priority.
 - This CPU priority boost effectively locks out an entire CPU. Which can be a good option to have in your toolbox.  
 - This tool effectively removes the CPU from your configuration. Note: Since 2010, PowerVM dynamic LPAR changes (DLPAR) are a safer way.
