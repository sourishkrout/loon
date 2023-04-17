## Luna 🐶 exploring AI 💡 with OpenAI's DALL-E

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
