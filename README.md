# Optimisation_MacOs
Enlarging networking buffers, quicker Safari, opening files and folder quicker, etc.

#################################################
# Enlarging networking buffers

From https://www.youtube.com/watch?v=UbYj2BzGNFg&t=185s
  sudo -s
    sysctl -w net.inet.tcp.recvspace=65536
# give net.inet.tcp.recvspace: 131072 -> 65536
sysctl -w net.inet.tcp.sendspace=65536
# give net.inet.tcp.sendspace: 131072 -> 65536
sysctl -w net.inet.tcp.delayed_ack=0
# give net.inet.tcp.delayed_ack: 3 -> 0

# (-w fichier = Vrai si le fichier existe et est accessible en écriture. # http://manpagesfr.free.fr/man/man1/bash.1.html)


# https://rsmith.home.xs4all.nl/freebsd/enlarging-networking-buffers.html
# In the hope of increasing networking performance, I’ve set the following sysctls in /etc/sysctl.conf;

# Increase send/receive buffer maximums from 256KB to 16MB.
# FreeBSD 7.x and later will auto-tune the size, but only up to the max.
net.inet.tcp.sendbuf_max=16777216
# marche pas meme avec sysctl -w 
net.inet.tcp.recvbuf_max=16777216
# marche pas meme avec sysctl -w 

# Double send/receive TCP datagram memory allocation.  This defines the
# amount of memory taken up by default *per socket*.
# net.inet.tcp.sendspace=65536
# Deja fait plus haut
sysctl -w net.inet.tcp.recvspace=131072
# Give net.inet.tcp.recvspace: 65536 -> 131072

# Enlarge buffers for BPF device.
# sysctl net.bpf.bufsize=65536
# deja fait plus haut
sysctl net.bpf.maxbufsize=524288
# marche pas

#################################################
#Afin d’afficher plus vite vos photos et autres fichiers lorsque vous utilisez l’aperçu, collez celle-ci et redémarrez votre mac.
defaults write -g QLPanelAnimationDuration -float 0

#Pour retrouver le comportement par defaut :
defaults delete -g QLPanelAnimationDuration

#################################################
#Pour supprimer toutes les transitions et afficher plus rapidement vos fichiers et dossiers, tapez :
defaults write com.apple.finder DisableAllAnimations -bool true; killall Finder
#En relançant le finder, les fichiers et apparaissent de façon plus rapide.

#Pour annuler :
defaults write com.apple.finder DisableAllAnimations -bool true; killall Finder


#################################################
# SAFARI
#Dans une fenêtre du Terminal, copiez la commande suivante pour accélèrer le chargement des pages web.
# https://www.reddit.com/r/apple/comments/4jvx69/some_osx_speed_up_tricks/
defaults write com.apple.Safari WebKitInitialTimedLayoutDelay 0.25

defaults write com.apple.Safari WebKitResourceTimedLayoutDelay 0.0001

#Désactivez le préchargement DNS pour accèler les pages avec la ligne de code suivante :
# https://www.cadeboite.fr/mac/mac-safari-5-lent-comment-accelerer-safari/
defaults write com.apple.safari WebKitDNSPrefetchingEnabled -boolean false

