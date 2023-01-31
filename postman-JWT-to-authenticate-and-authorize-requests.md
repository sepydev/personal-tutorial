# Using-JWT-to-authenticate-and-authorize-requests-in-Postman

Choose the edit option on the collection

![1](/images/1.png)


write the following code into the "pre-request scripts":
```
let email  = pm.variables.get("email");
let password = pm.variables.get("password");
let baseUrl = pm.variables.get("baseUrl");
pm.sendRequest({
      url:  baseUrl+`/sso/token/`,
      method: 'POST',
      header: {
        'Accept': 'application/json',
        'Content-Type': 'application/x-www-form-urlencoded'
      },
      body: {
          mode: 'urlencoded',
          urlencoded: [
            {key: "email", value: email},
            {key: "password", value: password}
        ]
      }
  }, function (err, res) {
        pm.globals.set("token", res.json().token);
  });
```
![2](/images/2.png)

In the variables tab, define the parameters as shown in the image below
![3](/images/3.png)

In the final step, make the following settings
![4](/images/4.png)
