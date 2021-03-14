# Optimisation_MacOs
Enlarging networking buffers, quicker Safari, opening files and folder quicker, etc.

## Enlarging networking buffers

From https://www.youtube.com/watch?v=UbYj2BzGNFg&t=185s

    sudo -s
    sysctl -w net.inet.tcp.recvspace=65536`
    # give net.inet.tcp.recvspace: 131072 -> 65536
    sysctl -w net.inet.tcp.sendspace=65536
    # give net.inet.tcp.sendspace: 131072 -> 65536
    sysctl -w net.inet.tcp.delayed_ack=0
    # give net.inet.tcp.delayed_ack: 3 -> 0

    # (-w fichier = True if the file exists and is writable. # explanations from http://manpagesfr.free.fr/man/man1/bash.1.html)

from https://rsmith.home.xs4all.nl/freebsd/enlarging-networking-buffers.html
    
    # In the hope of increasing networking performance, I’ve set the following sysctls in /etc/sysctl.conf;

    # Increase send/receive buffer maximums from 256KB to 16MB.
    # FreeBSD 7.x and later will auto-tune the size, but only up to the max.
    net.inet.tcp.sendbuf_max=16777216
    # didn't work even with sysctl -w 
    net.inet.tcp.recvbuf_max=16777216
    # didn't work even with sysctl -w 

    # Double send/receive TCP datagram memory allocation.  This defines the
    # amount of memory taken up by default *per socket*.
    # net.inet.tcp.sendspace=65536
    # Already done higher
    sysctl -w net.inet.tcp.recvspace=131072
    # Give net.inet.tcp.recvspace: 65536 -> 131072

    # Enlarge buffers for BPF device.
    # sysctl net.bpf.bufsize=65536
    # Already done higher
    sysctl net.bpf.maxbufsize=524288
    # didn't work

## View your photos and other files faster when using preview

    # In order to view your photos and other files faster when using the preview, paste this one and restart your mac.
    defaults write -g QLPanelAnimationDuration -float 0

    # To find the default behavior :
    defaults delete -g QLPanelAnimationDuration

## To remove all transitions and view your files and folders faster

    defaults write com.apple.finder DisableAllAnimations -bool true; killall Finder
    # By relaunching the finder, the files and appear faster.

    # To find the default behavior :
    defaults write com.apple.finder DisableAllAnimations -bool true; killall Finder

## SAFARI

    # In a Terminal window, copy the following command to speed up the loading of web pages.
    # from https://www.reddit.com/r/apple/comments/4jvx69/some_osx_speed_up_tricks/
    defaults write com.apple.Safari WebKitInitialTimedLayoutDelay 0.25

    defaults write com.apple.Safari WebKitResourceTimedLayoutDelay 0.0001

    # Disable DNS preloading to speed up pages with the following line of code :
    # from https://www.cadeboite.fr/mac/mac-safari-5-lent-comment-accelerer-safari/
    defaults write com.apple.safari WebKitDNSPrefetchingEnabled -boolean false

