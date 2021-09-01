# fedora-toolbox-custom-images
Repository with custom fedora toolbox images for various developments.

Official toolbox images https://github.com/containers/toolbox/tree/main/images


## Images
All images have following utilities: zsh, httpie, tmux, vim, jq, tmux (on top of utilities provided by base image).

* f34/java11 - contains Adopt Open JDK 11, Groovy 3.0.8, Gradle 7.2 and Maven 3.8.2
* f34/java16 - contains Adopt Open JDK 16, Groovy 3.0.8, Gradle 7.2 and Maven 3.8.2


## SDKMAN
In order to use SDKMAN in your toolbox, I did following:

1. I set env variable SDKMAN_DIR="/usr/local/sdkman" to make SDKMAN install binaries inside image.
2. I put this into my ~/.zshrc file, so SDKMAN is only initialized when I am running inside toolbox.
put that into your ~/.zshrc file

```
if [ -f /run/.toolboxenv ]; then
  export SDKMAN_DIR="/usr/local/sdkman"
[[ -s "/usr/local/sdkman/bin/sdkman-init.sh" ]] && source "/usr/local/sdkman/bin/sdkman-init.sh"
fi
```
