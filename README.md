# toolboxexamples
A few short examples of using [toolbox](https://github.com/containers/toolbox) containers to their fullest potential.

The past few days I have been playing around with using other Linux distributions in toolbox. It’s something I think of every once in a while. *Darn I’d really like a package from the AUR* or *Debian’s libraries would be useful now.* Fedora is close to perfect, but I am sometimes missing little things. In the past, I have used vanilla podman for things like that, but that can be complex, especially for doing rudimentary testing. So, I did some research, did some playing around, and got a few other OSes working in toolbox.

It’s nothing groundbreaking, and I’m sure it has been done better elsewhere, but if anyone has been interested and would like help or would like to help me, feel free to take a look.

## Basic usage:

*These images are highly unofficial and not very well tested. Please don't hesitate to open an issue if you run into any.*

To create the image, simple CD into the appropriate directory and build!

```sh
git clone https://github.com/nickavem/toolboxexamples.git
cd toolboxexamples
cd dockerfiles/base/alpbox
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

## FAQ

**Will you try to implement these images upstream?**
No. There is still a lot of work to be done on the upstream toolbox regarding
multi-distro support before this will even be probable.

**Will you publish these images to a registry (i.e., Docker hub)?**
Perhaps eventually, however currently I would still consider them too volatile to 
be “production ready”. I also ask that nobody publish them independently without
my permission, even if only for personal use.

**What are the supported architectures?**
Currently, only x86_64 is explicitly supported, however I am not against adding 
fixes to support other architectures.
