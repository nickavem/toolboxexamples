# toolboxexamples
A few short examples of using [toolbox](https://github.com/containers/toolbox) containers to their fullest potential.

The past few days I have been playing around with using other Linux distributions in toolbox. It’s something I think of every once in a while. Darn I’d really like a package from the AUR or Debian’s libraries would be useful right now. Fedora is close to perfect, but I am sometimes missing little things. In the past, I have used vanilla podman for things like that, but that can be complex, especially for doing rudimentary testing. So, I did some research, did some playing around, and got a few other OSes working in toolbox.

It’s nothing groundbreaking, and I’m sure it has been done better elsewhere, but if anyone has been interested and would like help and/or would like to help me, feel free to take a look.

## Basic usage:

*These images are highly unofficial and not very well tested. Feel free to open an issue if you run into any.*

To create the image, simple cd into the appropriate directory and build!

```sh
git clone https://github.com/nickavem/toolboxexamples.git
cd toolboxexamples
cd dockerfiles/alpbox
podman build -t alpbox .
```

This will create an image automatically hosted locally on your system. To create a toolbox container using it, simply run:

```sh
toolbox create --image alpbox
```

And you should be good to go! As with any other toolbox container, entering should be as easy as:
```sh
toolbox enter alpbox
```
