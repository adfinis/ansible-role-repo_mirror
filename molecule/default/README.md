# Molecule testing

## Requirements

You *need* podman. Docker is not supported.

## Usage

To test this role, you need to build the container image first:

`podman build -t localhost/bullseye_systemd .`

This to ensure systemd-related tests run through while molecule is running.
