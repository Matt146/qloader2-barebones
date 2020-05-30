# qloader2 Bare Bones

This project will show you how to set up a simple long mode kernel using qloader2, a bootloader designed to make getting your kernel up and running as quickly as possible while supporting many useful features, such as:


* support for echfs, ext2 and fat32
* support for the linux and stivale boot protocols

This project can be build using the host compiler on most linux distros, but it's recommended you set up a [cross compiler](https://osdev.wiki/tools:compilers:gcc:x86:generic)

## the stivale header
This structure must be present in the `.stivalehdr` section in order for your kernel to be loaded by stivale.

```c
    struct stivale_header {
        uint64_t stack;
        // Flags
        // bit 0   0 = text mode,   1 = graphics mode
        uint16_t flags;
        uint16_t framebuffer_width;
        uint16_t framebuffer_height;
        uint16_t framebuffer_bpp;
   } __attribute__((packed));
```

 The stack member is the stack pointer that will be loaded, the flags define information on how the kernel wants to be loaded, specifically the info on whether text mode or graphics mode should be enabled and if 5 level paging should be enabled. 

## where to go from here

The first thing you should do after booting from qloader2 is loading your own [GDT](https://osdev.wiki/x86:structures:gdt)