# toolboxexamples
A few short examples of using [toolbox](https://github.com/containers/toolbox) containers to their fullest potential.

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
