# details of go mod option
when you make `go get github.com/RomanOrlovDev/gomodenabled`
this data will be downloaded to GOPATH

then if you change anything in repo `https://github.com/RomanOrlovDev/gomodenabled`
it will NOT be reflected in you project where you are using this module
you have to do

`go get github.com/RomanOrlovDev/gomodenabled@<hash-commit-of-required-changes>`

It will amend go.mod with downloaded version. Downloaded version will be stored in 
GOPATH/pkg/mod/github.com/!roman!orlov!dev/...
It is also worth to note that you can use any package of downloaded github.com/RomanOrlovDev/gomodenabled

You can execute

`go clean -modcache`
it will remove `github.com/RomanOrlovDev/gomodenabled` from GOPATH/pkg

In regard of *indirect* work in go.mod:

we added simple lib require `github.com/pborman/uuid v1.2.1` which required generic google guid. 

In this case in `github.com/RomanOrlovDev/gomodenabled` go.mod already will contain
`// indirect` word for google uid and common (without `//indirect`) `github.com/pborman/uuid v1.2.1`

When you get dependency of `github.com/RomanOrlovDev/gomodenabled` then go.mod will have
two `//indirect` both for `github.com/pborman/uuid v1.2.1` and `github.com/google/uuid v1.0.0`.
It is clear that it is not possible to identify tree of dependencies.

In regard of when GO111MODULES="on" restricts usage of imports: it is simply not allowed
to import any package (side package, not native), go will throw an error while compiling