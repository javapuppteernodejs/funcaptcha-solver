# How to Solve Funcaptcha by Using Python and GO
![](https://assets.capsolver.com/prod/images/post/2024-04-26/27a5e40d-ccf3-4138-88cb-66f5f65daa42.png)

Due to the continuous development of online security measures, FunCaptcha has become an attractive and effective variant of CAPTCHA. However, solving FunCaptcha challenges manually is not only time-consuming but also detracts from the user experience. To solve this problem, advanced CAPTCHA decoders have revolutionised the way FunCaptcha challenges are solved. In this article, we will explore the fastest and convenient FunCaptcha solving service, and we will also provide sample code to teach you how to solve FunCaptcha via Python and Go in a smooth manner!


## Understanding FunCaptcha:
Funcaptcha is an innovative CAPTCHA technology developed by Arkose Labs. Unlike traditional CAPTCHAs, Funcaptcha incorporates interactive puzzles and games to differentiate between humans and bots. These engaging puzzles offer a fun experience for humans while posing a significant challenge for bots.
> Struggling with the repeated failure to completely solve the irritating captcha?
>
> Discover seamless automatic captcha solving with **Capsolver** AI-powered Auto Web Unblock technology!
>
> Claim Your [Free Trial](https://www.capsolver.com/)
> 
> 
> ## Bonus Code
> Plus a bonus code for top captcha solutions; [CapSolver](https://www.capsolver.com/): **WEBS**. After redeeming it, you will get an extra 5% bonus after each recharge, Unlimited
> 
> ![](https://assets.capsolver.com/prod/images/post/2024-03-29/fbc29472-886c-45b2-9eb2-2b307f6d9700.png)
## The Functionality of Funcaptcha:
When a user encounters a website employing Funcaptcha, they are presented with an interactive puzzle or game. These puzzles are designed to be easily solvable by humans but considerably more challenging for bots. Once the user successfully solves the Funcaptcha, they gain access to the website's content or features.

## The Significance of Funcaptcha:
Funcaptcha plays a crucial role in preventing automated attacks on websites. As bots become more sophisticated, traditional CAPTCHAs have become easier for them to bypass. Funcaptcha's interactive and dynamic nature makes it considerably more difficult for bots to crack, significantly enhancing website security.

## The Challenges Posed by Funcaptcha:
While Funcaptcha offers enhanced security, it can present challenges for users, particularly those who need to solve it repeatedly. The need to solve multiple captchas can be time-consuming and frustrating, especially for businesses that rely on efficient operations.

## How to Solve Funcaptcha by CapSolver
Capsolver stands out as the fastest FunCaptcha solving service in 2024,and it uses AI-powered Captcha Solving Algorithms, which result in faster solving speed and significantly reduced costs, providing an excellent developer experience.


### Creating a task for FunCaptcha
To solve FunCaptcha, the first step involves creating a task with the `createTask` method. 

This requires you to provide certain details like the type of task, the URL of the website using FunCaptcha, the public domain key, and more. Here's an overview of the task object structure:
```json
{
  "type": "FunCaptchaTask",
  "websiteURL": "URL of the website using FunCaptcha",
  "websitePublicKey": "Public domain key",
  "funcaptchaApiJSSubdomain": "A special subdomain of funcaptcha.com",
  "data": "Additional parameter that may be required by FunCaptcha",
  "proxy": "Proxy details",
  "userAgent": "Browser's User-Agent used in emulation"
}

```
You can send a POST request to create a task using the Capsolver API like this:

```json
{
  "clientKey":"YOUR_API_KEY",
  "task":
  {
    "type": "FunCaptchaTask",
    "websiteURL":"https://funcaptcha.com/",
    "websitePublicKey":"00000000-0000-0000-0000-000000000000"
    "proxy":"Your_own_proxy"
  }
}

```
Once you've submitted the task, you should receive a 'Task ID' in the response if it's successful
### Retrieving the result of the task
After you've created the task, you can retrieve the result using the `getTaskResult` method. Depending on the system load, the results can be obtained within an interval of 1 to 20 seconds.

Here's an example of a POST request to get the task result:
```json
POST https://api.capsolver.com/getTaskResult
Host: api.capsolver.com
Content-Type: application/json

{
  "clientKey": "YOUR_API_KEY",
  "taskId": "Task ID received from the createTask method"
}
```
Once the task status is ready, you should receive the result of the FunCaptcha challenge in the response
### Solving Funcaptcha with Python and Go using Capsolver SDK:
Capsolver also provides SDKs for Python and Go. This makes it easier to integrate Capsolver into your existing projects. Here's an example of how to use the Capsolver SDK 
```python
# pip install --upgrade capsolver
# export CAPSOLVER_API_KEY='...'

import capsolver

# capsolver.api_key = "..."
solution = capsolver.solve({
    "type": "FunCaptchaTask",
    "websitePublicKey": "",
    "websiteURL": "",
    "proxy": "ip:port:username:password"
})
```
```go
package main

import (
	"fmt"
	capsolver_go "github.com/capsolver/capsolver-go"
	"log"
)

func main() {
	// first you need to install sdk
	//go get github.com/capsolver/capsolver-go

	capSolver := capsolver_go.CapSolver{ApiKey: "..."}
	solution, err := capSolver.Solve(map[string]any{
		"type":             "FunCaptchaTaskProxyLess",
		"websiteURL":       "https://www.yourwebsite.com",
		"websitePublicKey": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
	})
	if err != nil {
		log.Fatal(err)
		return
	}
	fmt.Println(solution)
}
```


## How to Solve reCAPTCHA by Using Python and Go

The following sample code contains how to solve funcaptcha via Python and GO

```python
# pip install requests
import requests
import json
import time

# TODO: set your config
api_key = "YOUR_API_KEY"  # your api key of capsolver
public_key = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  # publicKey of your target site
page_url = "https://www.yourwebsite.com"  # page url of your target site
blob_data = ""  # optional, some sites require blob data


def capsolver():
    payload = {
        "clientKey": api_key,
        "task": {
            "type": 'FunCaptchaTaskProxyLess',
            "websitePublicKey": public_key,
            "websiteURL": page_url,
            "data": json.dumps({"blob": blob_data}) if blob_data else ''
        }
    }
    res = requests.post("https://api.capsolver.com/createTask", json=payload)
    resp = res.json()
    task_id = resp.get("taskId")
    if not task_id:
        print("Failed to create task:", res.text)
        return
    print(f"Got taskId: {task_id} / Getting result...")

    while True:
        time.sleep(1)  # delay
        payload = {"clientKey": api_key, "taskId": task_id}
        res = requests.post("https://api.capsolver.com/getTaskResult", json=payload)
        resp = res.json()
        status = resp.get("status")
        if status == "ready":
            return resp.get("solution", {}).get('token')
        if status == "failed" or resp.get("errorId"):
            print("Solve failed! response:", res.text)
            return


token = capsolver()
print(token)
```

```go
package main

import (
	"bytes"
	"context"
	"encoding/json"
	"errors"
	"fmt"
	"io"
	"net/http"
	"time"
)

type capSolverResponse struct {
	ErrorId          int32          `json:"errorId"`
	ErrorCode        string         `json:"errorCode"`
	ErrorDescription string         `json:"errorDescription"`
	TaskId           string         `json:"taskId"`
	Status           string         `json:"status"`
	Solution         map[string]any `json:"solution"`
}

func capSolver(ctx context.Context, apiKey string, taskData map[string]any) (*capSolverResponse, error) {
	uri := "https://api.capsolver.com/createTask"
	res, err := request(ctx, uri, map[string]any{
		"clientKey": apiKey,
		"task":      taskData,
	})
	if err != nil {
		return nil, err
	}
	if res.ErrorId == 1 {
		return nil, errors.New(res.ErrorDescription)
	}

	uri = "https://api.capsolver.com/getTaskResult"
	for {
		select {
		case <-ctx.Done():
			return res, errors.New("solve timeout")
		case <-time.After(time.Second):
			break
		}
		res, err = request(ctx, uri, map[string]any{
			"clientKey": apiKey,
			"taskId":    res.TaskId,
		})
		if err != nil {
			return nil, err
		}
		if res.ErrorId == 1 {
			return nil, errors.New(res.ErrorDescription)
		}
		if res.Status == "ready" {
			return res, err
		}
	}
}

func request(ctx context.Context, uri string, payload interface{}) (*capSolverResponse, error) {
	payloadBytes, err := json.Marshal(payload)
	if err != nil {
		return nil, err
	}
	req, err := http.NewRequestWithContext(ctx, "POST", uri, bytes.NewReader(payloadBytes))
	if err != nil {
		return nil, err
	}
	req.Header.Set("Content-Type", "application/json")
	client := &http.Client{}
	resp, err := client.Do(req)
	if err != nil {
		return nil, err
	}
	defer resp.Body.Close()
	responseData, err := io.ReadAll(resp.Body)
	if err != nil {
		return nil, err
	}
	capResponse := &capSolverResponse{}
	err = json.Unmarshal(responseData, capResponse)
	if err != nil {
		return nil, err
	}
	return capResponse, nil
}

func main() {
	apikey := "YOUR_API_KEY"
	ctx, cancel := context.WithTimeout(context.Background(), time.Second*120)
	defer cancel()

	res, err := capSolver(ctx, apikey, map[string]any{
		"type":             "FunCaptchaTaskProxyLess",
		"websiteURL":       "https://www.yourwebsite.com",
		"websitePublicKey": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
	})
	if err != nil {
		panic(err)
	}
	fmt.Println(res.Solution["token"])
}
```
## Conclusion  
In this article, we've explored how to solve FunCaptcha challenges using Python and Go, two powerful programming languages commonly used for web scraping and automation tasks. By leveraging libraries, frameworks, and CAPTCHA-solving services like CapSolver, developers can overcome FunCaptcha challenges programmatically, enabling seamless automation of web scraping workflows.






