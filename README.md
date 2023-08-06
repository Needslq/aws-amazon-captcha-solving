# How to Solve AWS WAF Captcha
![](https://assets.capsolver.com/prod/images/post/2023-07-12/b0e1e5aa-2fdc-4e6a-913e-2eddbbb53d13.png)

Before we start solving AWS WAF Captcha, there are some requirements and points that we need to be aware of:

## 🔒 Requirements:

- CapSolver Key
- Proxy (Optional)

**Proxy is optional, depends on the task type used, will be required / optional.**

## 📒 Points to be aware of:


- Ensure the validity of the website URL
To verify the authenticity of the website URL, ensure that it returns a 405 status code and the HTML contains elements like iv, key, and context.
- Triggering the AWS Captcha is necessary to access this URL.
- The URL should yield an HTML response comprising the key, iv, and context.
**As illustrated in these images, a matching URL will yield a 405 status code, and its HTML will include elements such as key, iv, and context.**
![](https://assets.capsolver.com/prod/images/post/2023-07-18/9c1538a2-5b9e-4c89-8b7a-2c4593ebfad6.png)
![](https://assets.capsolver.com/prod/images/post/2023-07-18/c5a39ab8-346c-4c89-863d-e25e4365ef70.png)
**- Save the url of the challenge script, context value, iv value and key value.**

To solve AWS WAF Captcha, follow our documentation. For this example, we will only use the required parameters. The task types for AWS WAF Captcha are:
- ``AntiAwsWafTaskProxyless``: This task type requires don't require your own proxy.
- ``AntiAwsWafTask``: This task type requires your own proxies.

In this case, the task type that will be used in this blog, will be `AntiAwsWafTaskProxyLess`.

## 📤 Step 1: Submit the information to Capsolver

```http
POST https://api.capsolver.com/createTask
{
 "clientKey":"yourapiKey",
 "task":
 {
 "type":"AntiAwsWafTaskProxyless",
 "websiteURL":"https://efw47fpad9.execute-api.us-east-1.amazonaws.com/latest",
  "awsKey":"key value",
  "awsIv":"iv value",
  "awsContext":"context value",
  "awsChallengeJS":"Url of the js challenge"
 }
}
```
This will return a response that contains `taskId`, save this value and submit to the step 2.

## 🔖 Step 2: Get the results
We will need to retrieve the ``getTaskResult`` method until the captcha is solved. Retrieve every 3-5s.
```http
POST https://api.capsolver.com/getTaskResult
Host: api.capsolver.com
Content-Type: application/json
{
 "clientKey":"YOUR_API_KEY",
 "taskId": "TASKID OF CREATETASK" //ID created by the createTask method
}
```
Captcha solution will look like:
![AWS CAPTCHA TOKEN SOLUTION](https://assets.capsolver.com/prod/images/post/2023-07-12/925dd643-d8b9-4a7b-923c-f0b0c897e04e.png)

**After the captcha has been solved, you need to create the cookie ``aws-waf-token`` and add the value that you got from capsolver response.**

In conclusion, solving AWS WAF Captcha can be a daunting task, but with the help of capsolver.com, it can be done quickly and efficiently. By following the steps outlined above, you can easily solve AWS WAF Captcha.

CapSolver Team 💜
    