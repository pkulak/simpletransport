## About

This is an http.RoundTripper (http://golang.org/pkg/net/http/#RoundTripper)
that doesn't bother with connection pooling, proxies, custom TLS configs, etc.
It adds reasonably strict read and request timeouts. It's intended to be used for
applications with high request volumes and long uptimes. It uses significantly
less resources than http.Transport in these applications.

## Installing

### Using *go get*

    $ go get github.com/pkulak/simpletransport/simpletransport

## Example

    import (
            "github.com/pkulak/simpletransport/simpletransport"
            "net/http"
            "time"
    )

    func main() {
        client := &http.Client{
            Transport: &simpletransport.SimpleTransport{
                ReadTimeout: 10 * time.Second,
                RequestTimeout: 15 * time.Second,
            },
        }
        ...
    }