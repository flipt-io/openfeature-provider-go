# Flipt OpenFeature Provider (Go)

[![CI](https://github.com/flipt-io/openfeature-provider-go/actions/workflows/ci.yml/badge.svg)](https://github.com/flipt-io/openfeature-provider-go/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/flipt-io/openfeature-provider-go/branch/main/graph/badge.svg?token=0X8OWMEV16)](https://codecov.io/gh/flipt-io/openfeature-provider-go)
![status](https://img.shields.io/badge/status-experimental-orange.svg)

[![OpenFeature Specification](https://img.shields.io/static/v1?label=OpenFeature%20Specification&message=v0.5.0&color=yellow)](https://github.com/open-feature/spec/tree/v0.5.0)
[![OpenFeature SDK](https://img.shields.io/static/v1?label=OpenFeature%20Golang%20SDK&message=v0.5.0&color=green)](https://github.com/open-feature/go-sdk)

This repository and package provides a [Flipt](https://github.com/flipt-io/flipt) [OpenFeature Provider](https://docs.openfeature.dev/docs/specification/sections/providers) for interacting with the Flipt service backend using the [OpenFeature Go SDK](https://github.com/open-feature/go-sdk).

From the [OpenFeature Specification](https://docs.openfeature.dev/docs/specification/sections/providers):

> Providers are the "translator" between the flag evaluation calls made in application code, and the flag management system that stores flags and in some cases evaluates flags.

## Requirements

- Go 1.16+
- A running instance of [Flipt](https://www.flipt.io/docs/installation)

## Usage

### Installation

```bash
go get github.com/flipt-io/openfeature-provider-go
```

### Example

```go
package main

import (
    "context"

    "github.com/flipt-io/openfeature-provider-go/pkg/provider/flipt"
    "github.com/open-feature/go-sdk/pkg/openfeature"
)


func main() {
    openfeature.SetProvider(flipt.NewProvider())

    client := openfeature.NewClient("my-app")
    value, err := client.BooleanValue(context.Background(), "v2_enabled", false, openfeature.EvaluationContext{
        TargetingKey: "tim@apple.com",
        Attributes: map[string]interface{}{
            "favorite_color": "blue",
        },
    })

    if err != nil {
        panic(err)
    }

    if value {
        // do something
    } else {
        // do something else
    }
}
```
