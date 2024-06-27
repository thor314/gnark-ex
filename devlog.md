
### run the code
copy past that shit and `go build && go run` ... missing deps:
#### take 1 - from the homepage of their docs - missing deps
```
	go get github.com/consensys/gnark-crypto/ecc/gurvy
	go get github.com/consensys/gnark-crypto/ecc/bls12-377/fr@v0.12.2-0.20240215234832-d72fcb379d3e
	go get github.com/consensys/gnark-crypto/ecc/bls12-377/fr@v0.12.2-0.20240215234832-d72fcb379d3e
	go get github.com/consensys/gnark-crypto/utils@v0.12.2-0.20240215234832-d72fcb379d3e
	go get github.com/consensys/gnark/constraint/solver@v0.10.0
	go get github.com/consensys/gnark/profile@v0.10.0

...

go: module github.com/consensys/gnark-crypto@upgrade found (v0.12.2-0.20240215234832-d72fcb379d3e), but does not contain package github.com/consensys/gnark-crypto/ecc/gurvy
```
gurvy no longer exists in that location, and their example link is broken but fear not

the examples on their repo surely work? 
#### take 2 - no main in the example
- https://github.com/Consensys/gnark/tree/master/examples/cubic
- issue: no main - how do i call this program? Oof!
- i can probably use the test to write a reasonable main tho
    - no 
- okay maybe i need to stop looking at https://hackmd.io/@gnark/gnark and look at their other docs page
- https://docs.gnark.consensys.io/HowTo/write/design_considerations
#### take 3 - complicated example plonk, but it has a driver
I thought gnark only did groth16? No, it does plonk too. But go back, to take 2, we can probably use the tests to write a driver, this looks way complicated
#### take 4 - different docs
- https://docs.gnark.consensys.io/overview
- ok we're doing mimc in this example now
```sh
> go build
# gnark-ex
./main.go:17:11: err declared and not used
./main.go:17:18: undefined: mimc
./main.go:17:35: api.Curve undefined (type frontend.API has no field or method Curve)
./main.go:21:47: undefined: cs

# ok try copying the compile circuit and create proof instructions
> go build
# gnark-ex
./main.go:17:11: err declared and not used
./main.go:17:18: undefined: mimc
./main.go:17:35: api.Curve undefined (type frontend.API has no field or method Curve)
./main.go:21:47: undefined: cs
./main.go:28:35: undefined: ecc
./main.go:28:46: undefined: r1cs
./main.go:34:51: undefined: ecc
./main.go:36:20: undefined: groth16
./main.go:37:19: undefined: groth16
./main.go:38:12: undefined: groth16
./main.go:38:12: too many errors
```
*fukin idiot*
