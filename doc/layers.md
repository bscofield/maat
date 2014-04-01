# Layers

Maat's infrastructure is *layered*; each layer can be treated differently.

## OS / system

This is the core of Maat's immutable infrastructure. Once an instance is launched, *nothing* at this level can be altered; we can only destroy and replace.

This includes OS patches, server configuration, and core utilities (e.g., rsyslog).

It's OK if it takes a while to update this layer. The process would involve building new base images with the updates, then using those as the foundation for new higher-level (library- or application-level) images that get deployed.

## Libraries / application utilities

For a Ruby application, this layer would include gems, as well as external libraries like, say, ImageMagick. Note that it may be useful to divide this layer along just those lines -- with external libraries changing less frequently than the in-language libraries.

During primary development, this layer essentially collapses into the application layer and can be ignored as an image source. Once the application is in production and is being used, however, this layer should be treated more like the system -- changes to it can take some time (less time than updating the system layer, though), and once a new image is built it can be used to regenerate new application-level images.

## Application

This is where the application lives; it's the most frequently updated (by orders of magnitude). As such, we build a new image for every commit that passes continuous integration (motivation to keep the test suite fast!). These images may be deployed or not.

Ideally, it should take < 2 minutes for a change to go live at the application level.
