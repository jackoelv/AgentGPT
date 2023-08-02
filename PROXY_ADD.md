# Add proxy support for special users.


1. docker-compose.yml
line 36:   
```
 http_proxy: "http://host.docker.internal:7890" # PROXY_ADD: For Windows only. If you are running on a linux server, you should set the address like http://172.18.0.1:7890 as your docker gateway address which is the localhost ip for docker.
```   
2. platform/pyproject.toml
line 37:
```
openai = { path = "../openai-0.27.8" }
```


3. cli/src/questions/newEnvQuestions.js
line 4:
```
//PROXY_ADD for localhost proxy here.
const { HttpsProxyAgent } = await import('https-proxy-agent');
const proxy = "http://127.0.0.1:7890";
const agent = new HttpsProxyAgent(proxy);
```

4. platform/Dockerfile
line 21:
```
COPY openai-0.27.8 /app/openai-0.27.8
```

Author: jackoelv
Email: jack.koe@gmail.com
