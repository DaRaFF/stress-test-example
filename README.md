# What is this repository for

This is a working example of how to setup a very simple stress test with a mocked api.

If you for example want to test how varnish caching behaves, you need a simple mocked api for a quick test.


# How to Start the Mock

* `nvm use v4.1.2` # you have to use node 4.*
* `npm install -g api-mock` # the mocking tool
* `api-mock ./api.md --port 80` # start the mocking server. The server response is defined in ./api.md
* Call `curl localhost:80` to make a quick test


# How to Make a Simple Stress Test


## Make a Stress Test with ab to your Mock (Senseless)
`ab -k -c 80 -n 2000 localhost:80`


## Make a Stress Test with ab to your Mock over a Varnish
* Use alpine-varnish https://github.com/njmittet/alpine-varnish for setting up varnish and start varnish on port 80
* `ab -k -c 80 -n 2000 localhost:8080`
* or just do a loop over a list of url's `while read url; sleep 0.01; do echo "localhost:8080${url}"; curl -s localhost:8080"${url}"; done < url-list.txt`
