# 🚀 Performance Boost : Enable GPU Hardware Acceleration on Linux (Browser / Video Playback)

## Short Intro,

It's been a while since I have written some **Linux stuff so h**ere we go, I guess many of you don't really know about this thing and just using Chromium-Based Browsers (i.e. Chrome and Brave) without getting the most performance of your system. You can often notice the performance lag while doing any GPU-intensive work or playing 4K Videos on your system. Basically,

> **Hardware acceleration** is the use of [computer hardware](https://en.wikipedia.org/wiki/Computer_hardware) designed to perform specific functions more efficiently when compared to [software](https://en.wikipedia.org/wiki/Software) running on a general-purpose [central processing unit](https://en.wikipedia.org/wiki/Central_processing_unit) (CPU).

When I discovered this thing a few years back I didn't find that much good documentation somewhere to get this working, But I tried and finally... **GET THIS WORKING on my system, so I am sharing with you the config which I used:**

Open Terminal and go here (or any other dir where your browser config files are saved, hope you can get that by yourself)

`nano ~/.config/brave-flags.conf`

(This will open that file in `nano` text editor)  
and paste the below CLI flags which will apply automatically while opening your Brave Browser. (Maybe Diff for yours)

CLI flags (e.g. `~/.config/brave-flags.conf`) should match approximately these:

```bash
--force-dark-mode
--enable-features=VaapiVideoEncoder,VaapiVideoDecoder,CanvasOopRasterization,TouchpadOverscrollHistoryNavigation,WebUIDarkMode
--enable-zero-copy
--use-gl=desktop    # =egl on wayland
--ignore-gpu-blocklist
--enable-oop-rasterization
--enable-raw-draw
--enable-gpu-compositing
--enable-gpu-rasterization
--enable-native-gpu-memory-buffers
--use-vulkan
--disable-features=UseChromeOSDirectVideoDecoder
--disable-sync-preferences
--force-device-scale-factor=1.5
--password-store=basic    # disables kwallet (optional)
```

Also, *optionally* enable these two flags by navigating into these addresses:  
`chrome://flags/#enable-raw-draw`  
`chrome://flags/#enable-vp9-kSVC-decode-acceleration`

Now everything should be green in `chrome://gpu` except for compositor rendering.

If not, possibly graphic drivers are missing, install appropriately for your GPU *(may require a reboot to take effect)*:

```bash
# Intel
sudo xbps-install mesa-intel-dri mesa-vaapi intel-video-accel
echo '[ -f /usr/lib64/dri/iHD_drv_video.so ] && export LIBVA_DRIVER_NAME=iHD' >> ~/.bashrc
echo 'if [ -f /usr/lib64/dri/iHD_drv_video.so ]; set -x LIBVA_DRIVER_NAME iHD; end' >> ~/.config/fish/config.fish

# AMD
sudo xbps-install mesa-ati-dri
```

Yet still, sometimes video decoding doesn't work, to check either go to

* Media section in chrome's inspect panel (F12/Right-Click)
    
* OR navigate to `chrome://media-internals`
    

while playing a video and see if the error is empty, `Hardware decoder: true` and `Decoding name: VDAVideoDecoder`.

![](https://animeshz.github.io/site/assets/battery-saving-video-decoding.c30735bc.jpg align="left")

![](https://animeshz.github.io/site/assets/battery-saving-video-decoding-true.e284433f.jpg align="left")

If not, first try using **an** [**enhanced-264ify**](https://chrome.google.com/webstore/detail/enhanced-h264ify/omkfmpieigblcllmkgbflkikinpkodlk) extension with the following blocks:

![enhanced-264ify extension](https://animeshz.github.io/site/assets/battery-saving-enhanced-264ify.055cfd66.jpg align="left")

That should make low-resolution videos (&lt;720p) forcefully use h264 which can be hardware-decoded.

If still not showing hardware decoding, you may need to build `intel-media-driver` with a nonfree kernel option (Or check if a nonfree repository on your distro redistributes this pkg) as pointed out by [**this comment**](https://github.com/saiarcot895/chromium-ubuntu-build/issues/98#issuecomment-757710499).

```bash
./xbps-src -o nonfree pkg intel-media-driver
```

### Other References:

* [https://wiki.archlinux.org/title/Hardware\_video\_acceleration](https://wiki.archlinux.org/title/Hardware_video_acceleration) <mark>(Arch Wiki </mark> 🛐<mark>)</mark>
    

* [https://www.youtube.com/watch?v=hoN78aUgOuM&t=50s](https://www.youtube.com/watch?v=hoN78aUgOuM&t=50s)
    
* [https://community.brave.com/t/no-hardware-video-decode-on-ubuntu-22-04/419576](https://community.brave.com/t/no-hardware-video-decode-on-ubuntu-22-04/419576)
    
* [https://community.brave.com/t/hardware-acceleration-enabled-but-doesnt-work/342912](https://community.brave.com/t/hardware-acceleration-enabled-but-doesnt-work/342912)
    
* [https://www.youtube.com/watch?v=5Y7-dRyFQ8s&t=218s](https://www.youtube.com/watch?v=5Y7-dRyFQ8s&t=218s)
    
* [https://www.youtube.com/watch?v=\_0o-xqQz7P0](https://www.youtube.com/watch?v=_0o-xqQz7P0) <mark>(For Firefox Users)</mark>
    

> #### **If you need more help or if this thing worked for you, let me know on** [**twitter**](https://twitter.com/ag@arunava)**, for more follow on hashnode (**@[Arunava Ghosh](@arunava) **)**