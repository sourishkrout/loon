## Luna 🐶 exploring AI 💡 with OpenAI's DALL-E

[![](https://badgen.net/badge/Open%20with/Runme/5B3ADF?icon=https://runme.dev/img/logo.svg)](https://runme.dev/api/runme?repository=https%3A%2F%2Fgithub.com%2Fsourishkrout%2Floon.git&fileToOpen=AI.md)

Do you have an OpenAI key?

```sh { interactive=false }
export OPENAI_API_KEY=Your key here
```

```sh { interactive=false mimeType=image/png }
cat hi_luna.png
```

What kinda scene description would you like for Luna?

```sh { interactive=false mimeType=text/x-json }
export SCENE="a happy shepherd surrounded by pizza"
export DALLE="$(curl https://api.openai.com/v1/images/edits \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -F image="@luna.png" \
  -F mask="@luna_mask.png" \
  -F prompt="$SCENE" \
  -F n=1 \
  -F size="512x512" \
  -s)"
echo $DALLE_EDITS | jq -c .
```

Give it a sec... OpenAI takes about ~20-40s to produce results.

```sh { interactive=false mimeType=image/png }
curl -Ns "$(echo $DALLE | jq -r '.data[0].url')"
```
