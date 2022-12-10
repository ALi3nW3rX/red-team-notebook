---
description: Simple Ping Sweeper Written in GO
---

# Ping Sweeper

```
package main

import (
    "fmt"
    "net"
    "os"
    "strconv"
    "time"
)

// ping sends a ping request to the provided IP address and returns
// true if a response is received within the timeout, and false otherwise.
func ping(ip string, timeout time.Duration) bool {
    addr, err := net.ResolveIPAddr("ip", ip)
    if err != nil {
        fmt.Println("Error:", err)
        os.Exit(1)
    }

    conn, err := net.DialIP("ip4:icmp", nil, addr)
    if err != nil {
        fmt.Println("Error:", err)
        os.Exit(1)
    }
    defer conn.Close()

    conn.SetDeadline(time.Now().Add(timeout))

    _, err = conn.Write([]byte(""))
    if err != nil {
        fmt.Println("Error:", err)
        os.Exit(1)
    }

    _, err = conn.Read(make([]byte, 1))
    if err != nil {
        return false
    }
    return true
}

func main() {
    if len(os.Args) != 2 {
        fmt.Println("Usage: ping_sweeper <IP address>")
        os.Exit(1)
    }

    ip := os.Args[1]
    timeout := time.Second

    // Check if the provided IP address is valid.
    if net.ParseIP(ip) == nil {
        fmt.Println("Error: Invalid IP address")
        os.Exit(1)
    }

    // Split the IP address into its components.
    parts := strings.Split(ip, ".")
    if len(parts) != 4 {
        fmt.Println("Error: Invalid IP address")
        os.Exit(1)
    }

    // Generate all possible combinations of the IP address.
    for i := 0; i < 256; i++ {
        for j := 0; j < 256; j++ {
            for k := 0; k < 256; k++ {
                for l := 0; l < 256; l++ {
                    addr := parts[0] + "." + parts[1] + "." + strconv.Itoa(i) + "." + strconv.Itoa(j) + "." + strconv.Itoa(k) + "." + strconv.Itoa(l)

                    // Check if the current combination is reachable.
                    if ping(addr, timeout) {
                        fmt.Println(addr, "is reachable")
                    }
                }
            }
        }
    }
}

```

To use this ping sweeper, compile it using the `go build` command and then run the resulting binary file, passing the IP address as an argument. For example:

```shell
$ go build ping_sweeper.go
$ ./ping_sweeper 192.168.1.0
```

This will generate all possible combinations of the provided IP address (e.g. 192.168.1.0, 192.168.1.
