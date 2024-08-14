# `tar`

This is a simple fork of `archive/tar` that adds a `Files()` method to `Reader` so you can use iterators.

```go
package main

import (
	"fmt"
	"os"

	"github.com/jonjohnsonjr/tar"
)

func main() {
	tr := tar.NewReader(os.Stdin)
	for hdr, err := range tr.Files() {
		if err != nil {
			panic(err)
		}

		fmt.Println(hdr.FileInfo().(fmt.Stringer).String())

		if n, err := io.Copy(io.Discard, tr); err != nil {
			panic(err)
		} else {
			fmt.Printf("read %d bytes\n", n)
		}
	}
}
```
