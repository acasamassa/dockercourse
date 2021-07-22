# Multi Stage Build

Allows us to use several FROM commands to build different and related images

Move to folder 07-MultiStageBuild

`cd 07-MultiStageBuild`

Build the first image:

`docker build --tag 07myapp:heavy -f dockerfile-heavy .`

Build the second image:

`docker build --tag 07myapp:light -f dockerfile-light .`

Check your images:

`docker images`