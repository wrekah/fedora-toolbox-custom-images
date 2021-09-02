# fedora-toolbox-custom-images
Repository with custom fedora toolbox images for various developments.

Official toolbox images https://github.com/containers/toolbox/tree/main/images

## Usage 
Given you have everything needed (Buildah, Podman, Toolbox), to build custom toolbox images you need:
1. git clone this repository
2. Build image of your choice, i.e. : ```buildah bud -f images/f34/java16/Containerfile -t fedora-toolbox-34-java16```
3. Create toolbox : ```toolbox create -i fedora-toolbox-34-java16```
4. Enter toolbox : ```toolbox enter fedora-toolbox-34-java16```

## Images
All images have following utilities: zsh, httpie, tmux, vim, jq, tmux (on top of utilities provided by base image).

* f34/java11 - contains Adopt Open JDK 11, Groovy 3.0.8, Gradle 7.2 and Maven 3.8.2
* f34/java16 - contains Adopt Open JDK 16, Groovy 3.0.8, Gradle 7.2 and Maven 3.8.2
* f34/node14-npm6 - contains nodejs 14.17.0 and npm 6.14.13
* f34/node16-npm7 - contains nodejs 16.5.0 and npm 7.19.1

## ZSH, settings and knowing whether you run in toolbox
I am using [starship prompt](https://starship.rs/). In default Fedora installation with bash, you get diamond sign when you enter toolbox. You can do something similar with starship prompt that lets you know if you run inside toolbox or not.

~/.config/starship.toml
```
[env_var.TOOLBOX_PATH]
format = "[🛠️]($style) "
```

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
