## Luna 🐶 exploring AI 💡 with OpenAI's DALL-E

Hi, I am Luna and I'm experimenting with generative AI via [runme.dev](https://runme.dev).

[![](https://badgen.net/badge/Open%20with/Runme/5B3ADF?icon=https://runme.dev/img/logo.svg)](https://runme.dev/api/runme?repository=https%3A%2F%2Fgithub.com%2Fsourishkrout%2Floon.git&fileToOpen=AI.md)

### Do you have an OpenAI key?

Please enter when prompted.

```sh { interactive=false }
export OPENAI_API_KEY=Your OpenAI key here
```

```sh { interactive=false mimeType=image/png }
cat hi_luna.png
```

### What kinda scene would you like? Enter when prompted.

```sh { interactive=false mimeType=text/x-json }
export SCENE="a happy german shepherd dog surrounded by pizza"
export DALLE="$(curl https://api.openai.com/v1/images/edits \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -F image="@luna.png" \
  -F mask="@luna_mask.png" \
  -F prompt="$SCENE" \
  -F n=1 \
  -F size="512x512" \
  -s)"
echo $DALLE | jq -c .
```

Give it a sec... OpenAI takes about ~20-40s to produce results.

```sh { interactive=false mimeType=image/png }
curl -s "$(echo $DALLE | jq -r '.data[0].url')"
```

## How it works

You basically give Dall-E two images:

1. The original image plus
2. A version of the same photo with roughly whatever you want to be replaced with generative imagery

Details are available in OpenAI's docs on [image edits](https://platform.openai.com/docs/guides/images/edits).

### Here are the two images included in the API request:

```sh { interactive=false mimeType=image/png }
cat luna.png # the original image
```

```sh { interactive=false mimeType=image/png }
cat luna_mask.png # surroundings removed with 100% alpha
```
