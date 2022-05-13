# Wishlist Lite

The lesser SSH directory ✨

I made this a little while after discovering the canonical [Wishlist](https://github.com/charmbracelet/wishlist), but after not getting it to work properly (it wasn't able to connect to any of my defined hosts) I still felt the need for a tool of this sort. This luckily coincided with the time I started learning about Go and after a bit of faffing about I got something to work!

## Installation

- using `go install`:

```bash
go install github.com/usrme/wishlistlite@latest
```

- build it yourself (requires Go 1.18+):

```bash
git clone https://github.com/usrme/wishlistlite.git
cd wishlistlite
go build
```

## Removal

```bash
rm -f "${GOPATH}/bin/wishlistlite"
rm -rf "${GOPATH}/pkg/mod/github.com/usrme/wishlistlite*"
```

## Usage

At the moment there is only one way to use it and that is to just execute `wishlistlite`. This opens up an alternate screen where you can (hopefully) see all of your hosts from your `~/.ssh/config` listed, which can then be SSH-ed into by selecting the appropriate one, or filtering for it, and pressing Enter. It then just grabs whatever is next to the `Host` declaration, precedes it with `ssh`, runs that executable, and exits `wishlistlite` leaving you with an SSH session.

It's also possible to press the letter `i`, which will allow you to supply a host to connect to on an ad-hoc basis. For example inputting `user@example.com` and pressing Enter will go through the exact process as above. Any of the entries from your SSH configuration are still valid as inputs.

### Caveats

Hosts starting with an asterisk are excluded as those (in my use case) usually mean either a `ProxyJump` or a `User` declaration right after.

Before starting the execution there is a verification that is made that the `ssh` executable exists, but there are still some other assumptions that are made:

- any necessary SSH keys are already loaded into an SSH agent;
- the SSH configuration is similar to this:

```text
Host tst001
  HostName tst001.example.com

Host tst002
  HostName tst002.example.com

Host tst003
  HostName tst003.example.com
```

## Acknowledgments

Couldn't have been possible without the work of people in [Charm](https://github.com/charmbracelet).

## License

[MIT](/LICENSE)