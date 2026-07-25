step 0:

- get ai llm inference provider account / api keys
- example: https://ollama.com/
- sign in
- go to settings -> keys -> create api key
- enter the name for the key -> generate api key -> copy to clipboard
  

step 1:

`pip install nanobot-ai`


step 2:

- open the secrets tab -> click new secret
- enter a name for the key -> paste the key you just copied from ollama -> click add secret

step 3: 
  - start the nanobot setup wizard with parameters to set the default workspace   directory and default config file. otherwise it will be set in /home/runner   .. and we want it in /home/runner/workspace

  ```
  nanobot onboard --workspace /home/runner/workspace --config /home/runner/workspace/.nanobot/config.json --wizard
  ```

step 3.5:

  - select provider
  - for ollama cloud, select custom / other OpenAI compatible provider
  - enter api .env variable key: `${YOUR_ENV_VARIABLE}`
  - enter ollama cloud url: `https://ollama.com/v1`
  - enter provider specific model name
  - ex:
  - ```nemotron-3-nano:30b-cloud```

  - enable gateway
  - enter a password for gateway access


step 4:
  - change web ui port so replit routes it properly.
  - in .nanobot/config.json

```
    "websocket": {
      "enabled": true,
      "host": "0.0.0.0",
      "port": 5000,
      "unixSocketPath": "",
      "path": "/",
      "token": "",
```

step 4.5:
- start the nanobot gateway with this command

```
nanobot gateway --workspace /home/runner/workspace --config /home/runner/workspace/.nanobot/config.json
```

(enter the password you set during the nanobot setup wizard)


step 5:

gitignore:
```
# nanobot memory files
memory/

# nanobot cron jobs
cron/

# nanobot webui files
.nanobot/webui/

# nanobot session history
sessions/
```

step 6:

set replit workflow command to this:

```
nanobot gateway --workspace /home/runner/workspace --config /home/runner/workspace/.nanobot/config.json
```

- workflows tab -> click new owrkflow -> name it 'run' -> select 'execute shell command' ->
- paste that in

now you can just click the run button instead of pasting that into shell every time


step 7:

done. 

EZ clap.


this is just the beginning. i will add more in the future. I still dont know how the cron jobs or dreams work yet. im not sure if i want to disable them or customize them yet.

next is setting up a flask server to create a custom "mcp" server and custom skills

and to figure out why this file isnt being tracked in git...