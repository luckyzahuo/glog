<p align="center">
    <a href="https://github.com/Higker/logker/"><img src="https://i.loli.net/2020/04/18/9JnSbmkist8dUaC.png" width="128"/></a>
    <h1 align="center">LogKer</h1>
</p>
<p align="center"><code>
logker</code> It's a log Library of Golang. It's easy to use.👨‍💻‍</p>

<p align="center">
    📚<a href="https://github.com/Higker/logker/blob/master/readme_zh.md" target="_blank">中文说明</a> | 
    🤩<a href="https://pkg.go.dev/github.com/higker/logker?tab=doc" target="_blank">pkg.go.dev</a> | 
    👨‍💻‍ <a href="https://github.com/Higker/logker/releases" target="_blank">Release</a> 
</p>

---

## Features

- Support file backup.
- Simple and easy to use.
- Support file storage log.
- Support console color printing.
- Custom log file storage location.
- Support setting time and time zone.
- Support log file size for split storage.
- Error level output to specified file separately.
- Four levels of `debug` `info` `error` `warning` are supported.
- `Future support: The remote computer stores the websoket output🙏.`
- `The project is constantly maintained and updated. I like 😍A kind of Please click star Thanks♪(･ω･)ﾉ!`
- Is this you?😜

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ge3na9rkzwg308c04oe5c.gif)

## Upgrade List
- [v1.1.5](https://github.com/Higker/logker/releases/tag/v1.1.5) Support for custom message formats  [issues1](https://github.com/Higker/logker/issues/1)


## Installation

🔝 The minimum requirement of Go version is **1.11**.
🔝 Your project also uses go module!!!

```shell script
go get github.com/Higker/logker
```
OR
```shell script
go get -u github.com/Higker/logker
```

command add `-u` flag to update in the future.

#### PS: if A kind of Tips:
```shell
$ go get github.com/Higker/logker
go: github.com/Higker/logker upgrade => v1.1.5
go get: github.com/Higker/logker@v1.1.5: parsing go.mod:
        module declares its path as: github.com/higker/logker
                but was required as: github.com/Higker/logker
```
##### You only need to modify the size of 'higker' in go.mod of your project
```json
module tets

go 1.14

require github.com/higker/logker v1.1.5 

```

## Use Example
#### 1. File Logger
```go
package main

import (
	klog "github.com/higker/logker"
	"time"
)

func main() {
	// Specify file location! Create folder in advance!!
	dir := "/Users/ding/Documents/test_log"
	// New file logger
	// File Max size : You can also use built-in constants
	// klog.GB1  	= 1GB
	// klog.MB10  	= 10MB
 	// klog.MB100	= 100MB
	format := "{level} - DATE {time}  - POS {position} - MSG {message}" //This version was modified from v 1.1.5
	flog := klog.NewFlog(klog.DEBUG, true, klog.Shanghai, dir, "log", 10*1024, 0777,format)
	// Analog output log
	for {
		flog.Debug("DEBUG : %d + %d = %d",1,2,1+2)
		flog.Error("ERROR")
		flog.Warning("WARNING %p",flog)
		flog.Info("INFO %s","Hello LogKer.")
		time.Sleep(2 * time.Second)
	}
}

```
> 👆Parameter note List:
```go

// Build File logger
// Args note
// logLevel:    lev,       \\ logging level
// wheError:    wheErr,    \\ whether enable  error alone file
// directory:   dir,	   \\ logging file save directory
// fileName:    fileName,  \\ logging save file name
// timeZone:    zone,	   \\ load time zone format
// power:       power,     \\ file system power
// fileMaxSize: size,      \\ logging alone file max size
// format :
	// Now upgrade to version v 1.1.5 to customize the message output format ~
	// TheCustomTagNameMustBe {level} {time} {position} {message}
	// The location of the custom label is the location
	// where the program outputs the corresponding log message at run time！！！！
	// forExampleHereIsMyCustom
	// 1. //format := "{level} - {time} - {position} - {message}"
```

#### 2. Console Logger

```go

package main

import (
	"github.com/higker/logker"
	"strings"
)

//type Formatting string

// logKer library Test
func main() {
	// Now upgrade to version v 1.1.5 to customize the message output format ~
	// TheCustomTagNameMustBe {level} {time} {position} {message}
	// The location of the custom label is the location
	// where the program outputs the corresponding log message at run time！！！！
	// forExampleHereIsMyCustom
	// 1. //format := "{level} - {time} - {position} - {message}"
	format := "{level} - 时间 {time}  - 位置 {position} - 消息 {message}" //This version was modified from v 1.1.5
	var log logker.Logger
	log = logker.NewClog(logker.DEBUG, logker.Shanghai, format)
	log.Debug("DEBUG %s","自定义日志消息匹配符测试")
	log.Info("%v", log)
	log.Warning("%v", logker.Shanghai)
	log.Error("ERROR")
}
```
## OutPut
```shell
[ DEBUG ] - 时间 2020-04-20 11:57:23.8927  - 位置 main.go|main.main:23 - 消息 DEBUG 自定义日志消息匹配符测试
[  INFO ] - 时间 2020-04-20 11:57:23.8928  - 位置 main.go|main.main:24 - 消息 &{0 Asia/Shanghai 0xc00008e220 {level} - 时间 {t位置 {position} - 消息 {message}}
[WARNING] - 时间 2020-04-20 11:57:23.8928  - 位置 main.go|main.main:25 - 消息 Asia/Shanghai
[ ERROR ] - 时间 2020-04-20 11:57:23.8929  - 位置 main.go|main.main:26 - 消息 ERROR

```
#### 3. Effect:
> The screenshot is not updated ~ The current screenshot is v1.0.9 version,
> you can install the library yourself to see the effect.
![LogKerGolang](https://i.loli.net/2020/04/18/Jjv82WDsyGtCaEH.png)

![log,golang,logKer](https://i.loli.net/2020/04/18/mJnvBp7oXwd8KSU.png)

## Thank list🤝
- fatih (https://github.com/fatih/color)
- Icon Mafia (Logo & Banner design)
- When are you? 😜

## Other 
- `Welcome to submit work order👏`
- `Pkg Docs: `[click to pkg.go.dev](https://pkg.go.dev/github.com/higker/logker?tab=doc)
## License

This project open source is MIT License
. See the [LICENSE](LICENSE) file content.
