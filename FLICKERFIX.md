# Fixing depricated IGPU patch for ASUS UX330UAR Hackintosh

(Taken from https://github.com/hieplpvip/ASUS-ZENBOOK-HACKINTOSH/issues/73#issuecomment-669553304)

This guide was written for people experiencing screen-flickering issues when using [@hieplpvip's][hieplpvip-url] [Guide to install macOS on Asus Zenbook](https://github.com/hieplpvip/asus-zenbook-hackintosh/wiki). Although this was written for the UX330UAR, it can be used for any other models experiencing screen-flickering issues. Simply edit the files for your model and use the right laptop base config for your Intel HD card at [RehabMan's Laptop Config Repo](https://github.com/RehabMan/OS-X-Clover-Laptop-Config). (If you're using another config because of your CPU/GPU, keep in mind the code snippets will not be the same).

To remove the SSDT IGPU patch, do the following: (This guide assumes you are following the [wiki instructions](https://github.com/hieplpvip/ASUS-ZENBOOK-HACKINTOSH/wiki/Basic-Instruction))

1. When you get to Step 2: Prepare USB, run the following instead

```
cd ~
git clone https://github.com/hieplpvip/ASUS-ZENBOOK-HACKINTOSH.git zenbook
cd zenbook
./download.sh
```

This will download the required kexts without compiling the ACPI (do not run `./make_acpi.sh`)

2. Find the file `SSDT-UX330-KabyLakeR.dsl`, which is the uncompiled .aml.
3. Open it and delete the line `#include 'include/SSDT-IGPU.dsl`
4. Proceed to run `./make_acpi.sh && ./make_config.sh` to finish building the required files.
5. Find `config_UX330-KabyLakeR.plist` in `build/config`
6. Download RehabMan's [config_HD615_620_630_640_650.plist](https://raw.githubusercontent.com/RehabMan/OS-X-Clover-Laptop-Config/master/config_HD615_620_630_640_650.plist)

We will still be using `config_UX330-KabyLakeR.plist` however we will edit it and add in the necessary parts of `config_HD615_620_630_640_650.plist`

7. Open `config_UX330-KabyLakeR.plist` and go to Devices ->FakeID and delete it
8. Then, copy FakeID AND Properties from`config_HD615_620_630_640_650.plist` -> Devices -> FaceID/Properties to your `config_UX330-KabyLakeR.plist`. This is what you want to copy over:

```
		<key>FakeID</key>
		<dict>
			<key>IntelGFX</key>
			<string>0x59168086</string>
		</dict>
		<key>Properties</key>
		<dict>
			<key>PciRoot(0)/Pci(0x02,0)</key>
			<dict>
				<key>AAPL,ig-platform-id</key>
				<data>AAAbWQ==</data>
				<key>device-id</key>
				<data>FlkAAA==</data>
				<key>#hda-gfx</key>
				<string>onboard-1</string>
				<key>#AAPL00,override-no-connect</key>
				<data></data>
				<key>#AAPL00,override-no-edid</key>
				<data></data>
				<key># DVMT-prealloc</key>
				<string>32MB BIOS, 19MB framebuffer, 9MB cursor bytes (credit RehabMan)</string>
				<key>framebuffer-patch-enable</key>
				<integer>1</integer>
				<key>framebuffer-stolenmem</key>
				<data>AAAwAQ==</data>
				<key>framebuffer-fbmem</key>
				<data>AACQAA==</data>
				<key>## @0 LVDS-&gt;DP</key>
				<string></string>
				<key>#framebuffer-con0-enable</key>
				<integer>1</integer>
				<key>#framebuffer-con0-type</key>
				<data>AAQAAA==</data>
				<key>## @1 HDMI</key>
				<string></string>
				<key>#framebuffer-con1-enable</key>
				<integer>1</integer>
				<key>#framebuffer-con1-type</key>
				<data>AAgAAA==</data>
				<key>#framebuffer-con1-flags</key>
				<data>hwEAAA==</data>
				<key>#framebuffer-con1-pipe</key>
				<data>EgAAAA==</data>
				<key>## @2 HDMI</key>
				<string></string>
				<key>#framebuffer-con2-enable</key>
				<integer>1</integer>
				<key>#framebuffer-con2-type</key>
				<data>AAgAAA==</data>
				<key>#framebuffer-con2-flags</key>
				<data>hwEAAA==</data>
				<key>#framebuffer-con2-pipe</key>
				<data>EgAAAA==</data>
				<key>## @3 HDMI</key>
				<string></string>
				<key>#framebuffer-con3-enable</key>
				<integer>1</integer>
				<key>#framebuffer-con3-type</key>
				<data>AAgAAA==</data>
				<key>#framebuffer-con3-flags</key>
				<data>hwEAAA==</data>
				<key>#framebuffer-con3-pipe</key>
				<data>EgAAAA==</data>
				<key>#1 0306-&gt;0105</key>
				<string>0x591b0000, 0105 instead of 0306, HDMI</string>
				<key>#1 framebuffer-con1-enable</key>
				<integer>1</integer>
				<key>#1 framebuffer-con1-alldata</key>
				<data>AQUKAAAIAACHAQAAAgQKAAAIAACHAQAA/wAAAAEAAAAgAAAA</data>
				<key>#2 0204-&gt;0105</key>
				<string>0x591b0000, 0105 instead of 0204, HDMI</string>
				<key>#2 framebuffer-con1-enable</key>
				<integer>1</integer>
				<key>#2 framebuffer-con1-alldata</key>
				<data>AQUKAAAIAACHAQAAAwYKAAAEAACHAQAA/wAAAAEAAAAgAAAA</data>
				<key>#3 no external</key>
				<string>0x591b0000, eliminate all external ports (0204 and 0306)</string>
				<key>#3 framebuffer-con1-enable</key>
				<integer>1</integer>
				<key>#3 framebuffer-con1-alldata</key>
				<data>/wAAAAEAAAAgAAAA/wAAAAEAAAAgAAAA/wAAAAEAAAAgAAAA</data>
			</dict>
			<key>PciRoot(0)/Pci(0x1f,3)</key>
			<dict>
				<key>#layout-id</key>
				<integer>3</integer>
				<key>#PinConfigurations</key>
				<data></data>
				<key>#hda-gfx</key>
				<string>onboard-1</string>
				<key>#no-controller-patch</key>
				<integer>1</integer>
			</dict>
		</dict>
```

9. Find the Graphics section in `config_UX330-KabyLakeR.plist` and replace it with the one in `config_HD615_620_630_640_650.plist`. It should look like this:

```
	<key>Graphics</key>
	<dict>
		<key>#EDID</key>
		<dict>
			<key>Inject</key>
			<false/>
		</dict>
		<key>#ig-platform-id</key>
		<string>0x591b0000</string>
		<key>Inject</key>
		<dict>
			<key>ATI</key>
			<true/>
			<key>Intel</key>
			<false/>
			<key>NVidia</key>
			<true/>
		</dict>
	</dict>
```

10. Make sure the SMBIOS ProductName property is set to MacBookPro14,1 and you have a valid SmUUID, SerialNumber and BoardSerialNumber
11. Follow the remaining steps on the [wiki](https://github.com/hieplpvip/ASUS-ZENBOOK-HACKINTOSH/wiki/Basic-Instruction)).

If you have any questions, post an issue on this repository and I'll try my best to help you out!

[hieplpvip-url]: https://github.com/hieplpvip
[asus-zenbook-hackintosh]: https://github.com/hieplpvip/ASUS-ZENBOOK-HACKINTOSH
