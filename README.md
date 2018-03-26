# Coreboot configuration for KGPE-D16

This is my personal config for coreboot on my KGPE-D16, along with the
resulting binaries.

I've put it up so that I've got a backup, and the necessary info to
reproduce my setup.

Flash this onto your own hardware at your own risk. I give no gaurantee that
you won't brick your device, so make sure you have a spare DIP-8 with a known
good BIOS, or an external programmer handy if it does not work out.

## What's special about these revisions?

Nothing in particular with the specific revisions, it is more that particular
releases gave me problems on my hardware.

The Libreboot release for this board is quite old at this point, and did not
boot consistently for me (hit bootloader on my disk maybe 50% of the time.)

Coreboot 4.7 release seemingly had ACPI issues for my processor (Opteron 6276),
which resulted in drastic performance decreases. `cpupower` was unable to
obtain a list of supported governors for the CPU, and could not detect the
correct supported frequencies.

Coreboot 4.6 release had issues booting consistently (approx. 90% of the time
failing to hit my bootloader). Kernel also reported performance problems with
interrupts, like this:

    [  202.558045] INFO: NMI handler (perf_event_nmi_handler) took too long to run: 11.982 msecs
    [  203.270599] perf interrupt took too long (32661 > 2500), lowering kernel.perf_event_max_sample_rate to 50000
    [  213.765389] perf interrupt took too long (32437 > 5000), lowering kernel.perf_event_max_sample_rate to 25000
    [  224.907326] perf interrupt took too long (32217 > 10000), lowering kernel.perf_event_max_sample_rate to 12500

These issues also appear in the `kernel_log.txt` of coreboot's automated board
status for the kgpe-d16 [which you can see here.](https://review.coreboot.org/cgit/board-status.git/tree/asus/kgpe-d16)

The revision I've picked here is from before the ACPI and interrupt performance
issues started to show up in the later 4.6 releases, but after the fixes that
appear to have remedied the boot consistency issues I had with the 4.6 release.

The SeaBIOS revision was just latest SeaBIOS at the time. I've included the
hash just to make the whole build possible to reproduce.

