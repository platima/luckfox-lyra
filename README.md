# Luckfox Lyra SD Card Images

This repository contains SD card images for various configurations of the Luckfox Lyra development board, including both Buildroot and Ubuntu-based systems.

These are built from the downloads available at the time, and have matching filenames, but do not require special software to image the TF/SD card with.

## Available Images

### Lyra (Base Model)
- Buildroot-based:
  - `Luckfox_Lyra_MicroSD_241230.img.bz2`
  - `Luckfox_Lyra_MicroSD_241230.img.sha256`
- Ubuntu-based:
  - `Luckfox_Lyra_Ubuntu_MicroSD_241230.img.bz2`
  - `Luckfox_Lyra_Ubuntu_MicroSD_241230.img.sha256`

### Lyra Plus
- Buildroot-based:
  - `Luckfox_Lyra_Plus_MicroSD_241230.img.bz2`
  - `Luckfox_Lyra_Plus_MicroSD_241230.img.sha256`
- Ubuntu-based:
  - `Luckfox_Lyra_Plus_Ubuntu_MicroSD_241230.img.bz2`
  - `Luckfox_Lyra_Plus_Ubuntu_MicroSD_241230.img.sha256`

## Usage

1. Download the appropriate image for your Luckfox Lyra board
2. Verify the SHA256 checksum of the uncompressed image using the provided .sha256 file
3. Extract the .bz2 file
4. Flash the image to your microSD card

## Verification

To verify your download after extraction:
```bash
sha256sum -c Luckfox_Lyra_MicroSD_241230.img.sha256```

## Image Details

- Buildroot images provide a minimal, fast-booting system optimized for embedded applications
- Ubuntu images offer a fuller glibc environment with additional packages and development tools

## Flashing Instructions
### Linux/macOS
```bunzip2 Luckfox_Lyra_MicroSD_241230.img.bz2
sudo dd if=Luckfox_Lyra_MicroSD_241230.img of=/dev/sdX bs=4M status=progress```

Replace /dev/sdX with your SD card device (can be found using lsblk command).

### Windows
Use Balena Etcher.

## Warning
Always verify you're using the correct device path before flashing. Using the wrong device path can result in data loss.

## Expanding Root Partition

After flashing, you may want to expand the root partition to use the full SD card space. You can do this using the provided Python script:

```bash
# Download the expansion script
wget https://raw.githubusercontent.com/[your-repo]/expand_partition.py

# Make it executable
chmod +x expand_partition.py

# Run as root (replace mmcblk0 with your device)
sudo ./expand_partition.py /dev/mmcblk0

# Update kernel partition table
sudo partx -u /dev/mmcblk0

# Expand the filesystem
sudo resize2fs /dev/mmcblk0p3
```

Note: If you're running this on the Lyra board itself, the device will typically be /dev/mmcblk0. If you're preparing the card on a PC with a card reader, the device might be something like /dev/sdX.

## Safety Checks
Before running the expansion:
1. Verify your device path using lsblk
2. Ensure you have a backup of important data
3. Make sure you're expanding the correct partition (usually partition 3)