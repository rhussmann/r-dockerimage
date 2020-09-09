# Example of using a base image to speed up initial Dockerfile creation

## Overview

This is an example of using base images to aid in speeding-up initial Dockerfile debugging and creation.

The general idea is, move things that seem to be working without tweaking into a base image (`Dockerfile.base`). Anything
you're currently working on and debugging should be in the `Dockerfile`. The `Dockerfile` is built on
top of the base image, so assume that all steps taken in the base image have been completed for the
derived image.

## Iteration

### Build the base image (only necessary when `Dockerfile.base` changes)
1. Move stable build steps into `Dockerfile.base`
2. Run `docker build -f Dockerfile.base -t rhussmann/r-base .`


### Build the derived image (this should be where most iteration occurs)
1. Make any changes to `Dockerfile`
2. Run `docker build -t rhussmann/r-custom .`
3. Expirment with your new image, `rhussmann/r-custom`
4. Repeat steps 1-3 as necessary

Once items in `Dockerfile` have become more stable, you can move those to `Dockerfile.base`, rebuild
the base image and keep on testing.
