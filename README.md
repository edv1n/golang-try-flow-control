# golang-try-flow-control
Golang proposal: nil detection and error handling with try keyword

## Objective

1. a way to scope `error` returned from a function which resturns more than 1 results.
2. generalize `try` keyword, so that it is not limited to error handling

## Example

```go

f1() (int, string, error) {}

func main() {
  a, s := try f1() with err { return err }
}

```

Problem: why `try` shall only check the last result, and return the non-last results? Moreover, the `with` syntax is special here.

```go

func main() {
  var v = byte(nil)
  
  try v {
    fmt.Println("v is nil")
  } else {
    fmt.Println("v is not nil")
  }
}

// result:
// v is nil
```

```go
func main() {
  try v := byte(nil); v {
    fmt.Println("v is nil")
  } else {
    fmt.Println("v is not nil")
  }
}

// result:
// v is nil
```

```go
f1() (int, string, error) {}

func main() {
  a, s, err := f1(); try err { return err }
}
```

## Problems with current error handling in Go

### No way to scope `error` if a function returns 2 results

For function which returns `error` only, we can

```go
if err := f(); err != nil {
  //handle error
  return nil, err
}

fmt.Println("%v", err) //undefined: err
```

However, for function which returns 2 results:

We usually handle err in following way

```go
a, b, err := f()
if err != nil {
  //handler error
  return nil, nil, err
}

fmt.Println("%v", err) // can compile, `err` is defined
```

### 
