[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stars][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![License][license-shield]][license-url]

<br />
<p align="center">
  <a href="https://github.com/andr-dev/ASUS-UX330UAR-Hackintosh/blob/master/assets/apple.png">
    <img src="assets/apple.png" alt="Logo" width="128" height="128">
  </a>

  <h3 align="center">ASUS-UX330UAR Hackintosh</h3>
</p>

## Table of Contents

- [About the Project](#about-the-project)
- [Specifications](#specifications)
- [Status](#status)
- [Usage](#usage)
- [Contact](#contact)
- [Acknowledgements](#acknowledgements)

## About The Project

About two years ago, I decided to attempt to hackintosh my ASUS-UX330UAR. After getting past the boot stage, I stumbled across [@hieplpvip's][hieplpvip-url] [ASUS Zenbook Hackintosh][asus-zenbook-hackintosh] repository which had the necessary ACPI patches, kext files, and [Clover][clover-url] config.plist needed for my Zenbook model (UX330UAR) as it was already supported. Unfortunately, I ran into many issues and after a couple months of effort, it seemed it would never work.

With the recent pandemic, I had more time to look into it and I decided to try once again. I was able to solve 90% of the issues and had one last one that seemed unfixable. For some reason, although my Intel HD 620 QE/CI was working as expected, the screen would flicker every once in a while. While it was managable at the beginning, as time went on, the frequency of the flickers would increase and become progressively worse to the point where the machine is unusable. Other users had experienced [this issue][flicker-issue-url] before but it seemed there was no fix.

Luckily, I was able to contact [@hieplpvip's][hieplpvip-url] and fix the issue, which I describe in further detail [here][flicker-issue-fix-url]. To sumarize, the graphics injection method being used, SSDT-IGPU patching, was depricated and seemed to be incompatible with newer versions of [WhateverGreen.kext][whatevergreen-url]. As such, the SSDT-IGPU patch needed to be removed from the compiled .aml and graphics properties injected in the config.plist.

With this small issue fixed, I got my ASUS-UX330UAR fully hackintoshed! As such, I decided to upload my config to help others trying to hackintosh their ASUS-UX330UAR.

WARNING: There is no guarantee this config will work for your system. Be careful if you are new to the hackintoshing community as you may accidentally brick your system or delete your files. Although there is virtually no risk of damaging any hardware components, anything is possible. Proceed with caution.

## Specifications

| Part           | Details                                  |
| -------------- | ---------------------------------------- |
| Computer Model | Asus UX330UAR                            |
| CPU            | Intel® Core™ i5 8250U Processor          |
| GRAPHICS       | Intel HD Graphics 620                    |
| RAM            | 8 GB LPDDR3 1866MHz SDRAM Onboard memory |
| DISPLAY        | 13.3" (16:9) FHD (1920x1080) 60Hz        |
| STORAGE        | 1 TB SATA 3.0 M.2 SSD (UPGRADED)         |
| WIFI           | Intel (R) Dual Band Wireless-AC 8260     |

## Status

This config supports everything the [ASUS Zenbook Hackintosh][asus-zenbook-hackintosh] repository supports and fixed the dreaded screen-flickering issue.

### Tested:

- **MacOS 10.15 Catalina**
- **Trackpad** with tap-to-click and multi-finger gestures
- **Keyboard** all keys work
- **Backlight** with the caps-lock and power-button indicator
- **FN Keys** with 16 levels of screen brightness, 16 levels of keyboard backlight, sleep, disable trackpad, mute, increase volume, and decrease volume keys
- **Power Management**
  - Fan speed changes based on CPU temperature
  - Fans automatically disable after being put to sleep
- **All USB Ports**
- **Webcam**
- **Wake on Lid Opening**

### Not Working:

- **Fingerprint Sensor**
  - No patch available, not that important anyways
- **Intel Wi-Fi** is still far from being supported
  - There are communities working on re-writing the Linux iwlwifi wifi driver into a MacOS kext at [AppleIntelWifiAdapter](https://github.com/zxystd/AppleIntelWifiAdapter) and [AppleIntelWifi](https://github.com/AppleIntelWifi/adapter) however both kexts are still very work in progress
  - **Solution:** Replace with a hackintosh-friendly wireless card like the DW1560
- **Intel Bluetooth** is still far from being supported
  - See post above, potentially stable kext available at [IntelBluetoothFirmware](https://github.com/OpenIntelWireless/IntelBluetoothFirmware)
- **SD Card Reader** will most likely work with some patching
  - Didn't bother to patch it since I barely use the SD Card Reader, more info for patching available at [How To Make a Generic Driver For Any Card Reader](https://www.tonymacx86.com/threads/how-to-make-a-generic-driver-for-any-card-reader.74471/)

### Not Tested:

- **Audio**
  - My UX330UAR's motherboard has an issue where the built-in audio does not work and thus I cannot test if audio works (both speakers / headphone jack and microphone). Audio, however, should be easy to patch and has been reported to work on similar systems.

## Usage

This config is provided more as a reference for those hoping to hackintosh their ASUS-UX330UAR. I do not recommend taking this config and using it on your system as it is better to build from source.

To do so, take a look at [@hieplpvip's][hieplpvip-url] [Guide to install macOS on Asus Zenbook](https://github.com/hieplpvip/ASUS-ZENBOOK-HACKINTOSH/wiki)

If you encounter the same screen-flickering issue as I did and/or want to patch graphics in a non-depricated way, follow [these instructions][flicker-fix-url].

## Contact

You can contact me at [abene1asus@gmail.com](mailto:abene1asus@gmail.com) if you have any questions about this specific model. I would recommend however contacting [@hieplpvip][hieplpvip-url] through Github (he's the real genius who made the ACPI patches and ASUS-specific kexts).

## Acknowledgements

Huge thanks to [@hieplpvip][hieplpvip-url] for not only spending over a year to manually create ACPI patches for his zenbook laptop and other zenbook models but for also helping me find the graphics fix to get my system fully functioning! He also made [AsusSMC.kext][asus-smckext] which enables native ALS support, keyboard backlight and FN keys on Asus laptops when paired with his patched DSDTs. Here is the [link][asus-zenbook-hackintosh] to his Zenbook Hackintosh repository.

Also thanks to all the developers who have spent countless years making the kexts necessary to enable hackintoshes to exist (and apple for making MacOS).

[contributors-shield]: https://img.shields.io/github/contributors/andr-dev/ASUS-UX330UAR-Hackintosh.svg?style=flat-square
[contributors-url]: https://github.com/andr-dev/ASUS-UX330UAR-Hackintosh/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/andr-dev/ASUS-UX330UAR-Hackintosh.svg?style=flat-square
[forks-url]: https://github.com/andr-dev/ASUS-UX330UAR-Hackintosh/network/members
[stars-shield]: https://img.shields.io/github/stars/andr-dev/ASUS-UX330UAR-Hackintosh.svg?style=flat-square
[stars-url]: https://github.com/andr-dev/ASUS-UX330UAR-Hackintosh/stargazers
[issues-shield]: https://img.shields.io/github/issues/andr-dev/ASUS-UX330UAR-Hackintosh.svg?style=flat-square
[issues-url]: https://github.com/andr-dev/ASUS-UX330UAR-Hackintosh/issues
[license-shield]: https://img.shields.io/github/license/andr-dev/ASUS-UX330UAR-Hackintosh.svg?style=flat-square
[license-url]: https://github.com/andr-dev/ASUS-UX330UAR-Hackintosh/blob/master/LICENSE.txt
[flicker-fix-url]: https://github.com/andr-dev/ASUS-UX330UAR-Hackintosh/blob/master/FLICKERFIX.md
[hieplpvip-url]: https://github.com/hieplpvip
[asus-zenbook-hackintosh]: https://github.com/hieplpvip/ASUS-ZENBOOK-HACKINTOSH
[asus-smckext]: https://github.com/hieplpvip/AsusSMC
[clover-url]: http://cloverefiboot.sourceforge.net/
[flicker-issue-url]: https://www.tonymacx86.com/threads/guide-asus-zenbook-using-clover-uefi-hotpatch.257448/post-1878623
[flicker-issue-fix-url]: https://github.com/hieplpvip/ASUS-ZENBOOK-HACKINTOSH/issues/73#issuecomment-669553304
[whatevergreen-url]: https://github.com/acidanthera/WhateverGreen
