# Kent Network Website

Website for Kent Network


## Build instructions

You will need a working install of Go and Hugo. I'm using the current
dev version installed with `go get`.

`go get -v github.com/gohugoio/hugo`

The website can be built using `hugo` and it can be served locally
using `hugo serve` and viewed locally
at [http://localhost:1313/](http://localhost:1313/)

If you want to expose the website to the network (e.g. to test on a
mobile device) set the bind address to `0.0.0.0`

`hugo serve --bind 0.0.0.0`


## Useful notes:
Brand colour `#37a3ff`.
