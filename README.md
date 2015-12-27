# docker-run-build
Incrementally build Docker images.

## Installation

    pip install docker-run-build

## Usage

    Usage: docker-run-build [OPTIONS] IMAGE

    Options:
    --output TEXT         output image
    --no-assert-hostname  Disable hostname validation
    --mount TEXT          Mount volume (format: "src:target[:rw,:ro]")
    --help                Show this message and exit.

## Example

    $ docker-run-build ORIGINAL_IMAGE --output NEW_IMAGE <<EOF
    touch /tmp/FOOBAR
    EOF
    
    Updating image ORIGINAL_IMAGE (to: NEW_IMAGE)
    Running code..., output:
    Nothing
    
Now you can check that the file `/tmp/FOOBAR` exists in `NEW_IMAGE`:

    $ docker run -it NEW_IMAGE ls -l /tmp/FOOBAR

If you omit the `--output` parameter, the `ORIGINAL_IMAGE` will be replaced.

## Mounting volumes

You can use the `--mount` option to mount volumes during the run step:

    $ docker-run-build ORIGINAL_IMAGE --mount /home/user1/:/mnt/vol1:rw <<EOF
    cp /mnt/vol1/*.py /app/
    EOF
