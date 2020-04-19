# Go

## Simple Worker Pool

```
package main

import (
	"fmt"
	"time"
	"sync"
)

func main() {
	var wg sync.WaitGroup
	ch := make(chan int, 5)
	
	for i :=0; i < 5; i++ { 
		go func() { 
			for { 
				DoWork(<-ch)
				wg.Done()
			} 
		}()
	} 
	
	for i := 0; i < 20; i++ { 
		wg.Add(1)
		ch <- i
	}
	
	wg.Wait()
	
}
  
func DoWork(n int) {
	fmt.Println("Do work", n)
	time.Sleep(50 * time.Millisecond)
}
```
