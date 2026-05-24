# NullOS - Community Edition

> A community-driven fork of [NullOS](https://github.com/SussyNade/NullOS) — the AI-generated operating system experiment.

## What is this?

NullOS CE is a fork of NullOS where **humans are welcome to contribute**. The original NullOS is a pure experiment to see how far AI can go building an OS from scratch — every line written by Claude. This fork exists so the community can take that foundation and push it further, fix bugs, add features, and explore OS development together.

## Difference from the original

| | NullOS (original) | NullOS CE |
|-|-------------------|-----------|
| Code written by | AI only (Claude) | Anyone |
| Purpose | AI experiment | Community OS dev |
| Contributions | Closed | Open |
| Follows original | Yes | Diverges over time |

## Current status

| Phase | Description | Status |
|-------|-------------|--------|
| 0 | Bootloader + VGA output | ✅ Done |
| 1 | GDT, IDT, Interrupts | ✅ Done |
| 2 | Memory management (PMM + VMM) | ✅ Done |
| 3 | Processes + scheduler | 🔄 In progress |
| 4 | Filesystem + VFS | ⏳ Planned |
| 5 | Syscalls + userland | ⏳ Planned |
| 6 | Shell (nullsh) | ⏳ Planned |
| 7 | Basic networking | ⏳ Planned |
| 8 | GUI | ⏳ Planned |
| 9 | User applications | ⏳ Planned |

## Contributing

All contributions are welcome! Bug fixes, new features, documentation, anything.

1. Fork this repo
2. Create a branch: `git checkout -b feat/my-feature`
3. Commit your changes: `git commit -m "feat: my feature"`
4. Push: `git push origin feat/my-feature`
5. Open a Pull Request

### Good first issues
- Fix IDT triple fault bug
- Add serial port debug output
- Improve VGA driver (scrolling, more colors)
- Write more documentation

## Building

```bash
git clone https://github.com/SussyNade/NullOS-CE.git
cd NullOS-CE

docker run -it --rm -u root -v $(pwd):/nullos:z randomdude/gcc-cross-x86_64-elf
# Inside container:
apt-get install -y nasm grub-pc-bin grub-common xorriso mtools -q
cd /nullos/tools && make
exit

qemu-system-x86_64 -cdrom build/nullos.iso -m 256M -no-reboot -no-shutdown -display sdl
```

## Project structure

```
nullos/
├── boot/
│   ├── boot.asm       # Multiboot2 entry point
│   └── linker.ld      # Linker script
├── kernel/
│   ├── main.c         # kmain()
│   ├── gdt.c/h        # Global Descriptor Table
│   ├── idt.c/h        # Interrupt Descriptor Table
│   ├── pic.c/h        # PIC 8259 remapping
│   ├── timer.c/h      # PIT timer
│   ├── keyboard.c/h   # PS/2 keyboard driver
│   └── drivers/
│       └── vga.c/h    # VGA text mode 80x25
└── tools/
    ├── Makefile
    └── grub.cfg
```

## Tech stack

| | |
|-|-|
| **Language** | C99 + x86 Assembly (NASM) |
| **Bootloader** | GRUB2 (Multiboot2) |
| **Testing** | QEMU |
| **Cross-compiler** | x86_64-elf-gcc |

## License

MIT — do whatever you want with it.

## Related

- [NullOS (original)](https://github.com/SussyNade/NullOS) — the pure AI experiment
