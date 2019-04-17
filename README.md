[![Build Status](https://travis-ci.org/shogo82148/goacors.svg?branch=master)](https://travis-ci.org/shogo82148/goacors)
[![Coverage Status](https://coveralls.io/repos/github/shogo82148/goacors/badge.svg?branch=master&service=github)](https://coveralls.io/github/shogo82148/goacors?branch=master) [![GoDoc](https://godoc.org/github.com/shogo82148/goacors?status.svg)](https://godoc.org/github.com/shogo82148/goacors)  

# goacors
a cors-header middleware for goa(https://github.com/goadesign/goa).
This is a fork of https://github.com/istyle-inc/goacors

# how to use
1. `go get github.com/shogo82148/goacors`
2. write your main.go generated automatically from goagen.

	```
	service.Use(goacors.WithConfig(service, &goacors.DefaultGoaCORSConfig))
	```

		or

	```
	service.Use(goacors.WithConfig(service, &goacors.GoaCORSConfig{
		AllowOrigins: []string{"http://example.com"},
		AllowMethods: []string{goacors.GET},
	}))
		```

# Intermediate Match Mode

Intermediate Match Mode is using match logic allow wildcard in host, like `*.example.com`.

```
NOTIFY

Note that using wild card is not correct for specification of CORS.
And this mode is not recommended for production use.
I implemented this for only testing.
```

## how to use Intermediate Match Mode
To use this mode, you can use goacors.WithConfig like below,

```
service.Use(goacors.WithConfig(service, &goacors.GoaCORSConfig{
	AllowOrigins:     []string{"http://example.com"},
	AllowMethods:     []string{goacors.GET},
	DomainStrategy:   goacors.AllowIntermediateMatch,
}))
```

`DomainStrategy` option is added for this. default is `goacors.AllowStrict` and you need to change this to `goacors.AllowIntermediateMatch`

