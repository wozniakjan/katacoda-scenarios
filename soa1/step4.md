## Task 4

Let's split the big, fat monolith into slimmer services. Dirs `hello` and `auth` contain the source code for these two services. Check it out and play with it.

```
go build -o ./bin/hello ./hello
./bin/hello -http ":10080" -health ":10081"
```

In another terminal tab

```
go build -o ./bin/auth ./auth/
./bin/auth -http ":10090" -health ":10091"
```
