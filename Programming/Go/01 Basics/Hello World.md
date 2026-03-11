```go
package main

import "fmt"

func main() {
    fmt.Println("Hello World!")
}
```

# Explanation

This Go program prints **"Hello World!"** to the console. It demonstrates the basic structure of a standalone Go program.

## Breakdown

- **`package main`**  
  Declares that this file is a standalone executable program. Every Go program that runs must have a `main` package.

- **`import "fmt"`**  
  Imports Go's **fmt** package, which provides functions for formatted input and output. Here, it allows us to use `Println`.

- **`func main()`**  
  The entry point of the program. Execution starts here.

- **`fmt.Println("Hello World!")`**  
  Calls the `Println` function to display text on the console. This prints exactly: `Hello World!`

## Key Points / Notes

- Every standalone Go program requires a `main` package and a `main()` function.  
- This example shows the minimal working Go program structure.  
- Perfect for beginners to understand program flow and basic I/O in Go.

