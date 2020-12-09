# Modules
* init new project `go mod init` or `go mod init projectname` will create `go.mod` (something like package.json with package-lock.json)
* add dependency `go get` (version provided is not exact version but minimum version)
  * untill package is not used, it is marked as `// indirect`
  * `go mod tidy` - should be run before anything else
    * add any demendencies needed for other combination of OS 
    * to clear indirect (unused) modules run 