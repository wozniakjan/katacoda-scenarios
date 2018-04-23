## Task 3

Play with the monolith. Read the source code and try to understand it. Feel free to ask for help. Use password: 'password'.

```
sudo ./bin/monolith -http 0.0.0.0:10080
curl localhost:10080
curl localhost:10080/secure
curl localhost:10080/login -u user
curl -H "Authorization: Bearer $token" localhost:10080/secure
```

Go and read the [Twelve-Factor Apps](https://12factor.net/) guide. It's a set of best-practices for building deployable software-as-a-service apps / web apps. Which of these recommendations does the code follow?
