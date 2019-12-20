# go-diawi

Package written in go to interface with [diawi](https://www.diawi.com/)'s API

## Disclaimer
This repo was forked and modified to be used in the company I'm working. If you use Diawi and feel the changes I've made here work for you, go ahead and use it. If not, I strongly advise you to fork [sirkaiserkai/go-diawi](https://github.com/sirkaiserkai/go-diawi) and make your changes.

## Install

```sh
go get github.com/jotape26/go-diawi
```

## Example

Simply replace the diawi 'token' variable with your token string and replace the 'file' variable with the filename of your application.
```go
package main

import (
  gd "github.com/sirkaiserkai/go-diawi"
  "log"
)

func main() {
  token := "Your diawi token here"
  file := "App"
  
  uploadRequest := gd.NewUploadRequest(token, file)
  
  uploadResponse, err := uploadRequest.Upload()
  if err != nil {
    log.Fatal(err)
  }
  
  statusRequest := gd.NewStatusRequest(token, uploadResponse.JobIdentifier)
  
  statusResponse, err := statusRequest.WaitForFinishedStatus()
  if err != nil {
    log.Fatal(err)
  }
  
  log.Println(statusResponse)
}
```
  
