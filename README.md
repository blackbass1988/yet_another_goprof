# yet_another_pprof_wrapper


```go
package main

import (
	"flag"
	"fmt"
	"os"
	"time"

	yag "github.com/blackbass1988/yet_another_pprof_wrapper"
)

func main() {

	var (
		cpuProfile, heapProfile string
	)

	flag.StringVar(&cpuProfile, "cpuprofile", "", "Write the cpu heapProfile to `filename`")
	flag.StringVar(&heapProfile, "heapprofile", "", "enable heap profiling")
	flag.Parse()

	if cpuProfile != "" {
		cWriter, err := os.Create(cpuProfile)
		if err != nil {
			panic(err)
		}
		go yag.ProfileCpu(cWriter)
	}

	if heapProfile != "" {
		mWriter, err := os.Create(heapProfile)
		if err != nil {
			panic(err)
		}
		go yag.ProfileMemory(mWriter, 10*time.Second, true)
	}

	//do your stuff

	t := time.NewTicker(100 * time.Millisecond)

	data := make([]bool, 10)
	for _ = range t.C {
		data = append(data, true)
	}

	fmt.Printf("%+v", data)
}

```
