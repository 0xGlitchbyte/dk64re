## TODO:
- [ ] Setup RetroArch with LibRetroReversing
- [ ] Write a script to break apart asm.s file
- [ ] 

---
## Tools used:
- [n64split](https://github.com/queueRAM/sm64tools)
- [m2c](https://github.com/matt-kempster/m2c)
- [ImHex](https://github.com/WerWolv/ImHex)
  - [hexpyt](https://github.com/Calcoph/hexpyt)
--- 
## Notes:

- Downloaded/installed `n64split`
  - `git clone https://github.com/queueRAM/sm64tools`
  - `brew update && brew install capstone libyaml libpng coreutils make pkg-config tehzz/n64-dev/mips64-elf-binutils`
  - `export C_INCLUDE_PATH=../sm64tools:/opt/homebrew/Cellar/capstone/4.0.2/include/:/opt/homebrew/Cellar/libyaml/0.2.1/include:/opt/homebrew/Cellar/libpng/1.67/include`
  - Downloaded/installed `stb_image.h`
  `git clone https://github.com/nothings/stb`
  - exported `stb` to `C_INCLUDE_PATH` and `LIBRARY_PATH`
  - `make`

- Created new `n64split` yaml config 
```yaml
# ROM splitter configuration file
name: "Your Game Name (Region)"

# checksums from ROM header offsets 0x10 and 0x14
# used for auto configuration detection
checksum1: 0xA03CF036
checksum2: 0xBCC1C5D2

# base filename used for outputs - [please, no spaces)
basename: "yourGameName.region"

# ranges to split the ROM into
# types:
#   asm      - MIPS assembly block.  Symbol names are in 'labels' list below
#   behavior - behavior script
#   bin      - raw binary, usually data
#   header   - ROM header block
#   instrset - instrument set
#   level    - level commands
#   m64      - M64 music sequence bank
#   mio0     - MIO0 compressed data block.  may have texture breakdown
#   ptr      - RAM address or ROM offset pointer
#
#   textures types:
#      rgba   - 16-bit RGBA - [5-5-5-1)
#      ia     - 16/8/4/1-bit greyscale
#      skybox - grid of 32x32 16-bit RGBA
ranges:
   # start,  end,      type,     label
   - [0x000000, 0x000040, "header", "header"]
   - [0x000040, 0x001000, "bin",    "boot"]
   - [0x001000, 0x0B6A40, "asm", "main", 0x80241800]
# Labels for functions or data memory addresses
# All label addresses are RAM addresses
# Order does not matter
labels:
  - [0x80241800, "EntryPoint"]

```

- Installed RetroArch and got that working just fine
  - `brew install retroarch`
  - TODO: install LibRetroReversing for RetroArch

- Downloaded/installed `m2c`:
  - `git clone https://github.com/matt-kempster/m2c`
  - `python3 -m pip install --upgrade pycparser`

