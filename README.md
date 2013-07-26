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

    package main

    import (
        "fmt"
        "github.com/pkulak/simpletransport/simpletransport"
        "io/ioutil"
        "net/http"
        "time"
    )

    func main() {
        client := &http.Client{
            Transport: &simpletransport.SimpleTransport{
                ReadTimeout:    10 * time.Second,
                RequestTimeout: 15 * time.Second,
            },
        }

        resp, _ := client.Get("http://jsonip.com")
        body, _ := ioutil.ReadAll(resp.Body)
        resp.Body.Close()
        fmt.Println(string(body))
    }