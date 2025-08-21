*Words carry semantic information. Similar to how people can infer meaning based on a word's context, AI can derive representations for words based on their context too! However, the kinds of meaning that a model uses may not match ours. We've found a pair of AIs speaking in metaphors that we can't make any sense of! The embedding model is glove-twitter-25. Note that the flag should be fully ASCII and starts with 'htb{'.*
# Solution
So to put it simply, we can take this sentence.
>We've found a pair of AIs speaking in metaphors that we can't make any sense of!

It means the challenge file we are given is supposedly a talk between two AIs. Also they're speaking in a certain way which means this part where the AIs are using the model `glove-twitter-25`.
>The embedding model is glove-twitter-25.

If we check the challenge file, it's seems to be in the form of an analogy.
```
Like non-mainstream is to efl, battery-powered is to?
Like sycophancy is to بالشهادة, cont is to?
Like беспощадно is to indépendance, rs is to?
Like ajaajjajaja is to hahahahahahahahaahah, ２ is to?
Like bahno is to arbus, duit is to?
...
```

Now one of the capabilities of the glove model is to find semantic relationships. Hence the beginning of the challenge description.
> Words carry semantic information. Similar to how people can infer meaning based on a word's context, AI can derive representations for words based on their context too! However, the kinds of meaning that a model uses may not match ours.

From this understanding, we can assume that we need to finish the analogy by using the model `glove-twitter-25` and supposedly the given model output will give us the flag. Here's my script.
```
import modal

# Use a base image and install dependencies with prebuilt wheels
image = (
    modal.Image.debian_slim(python_version="3.12")
    .pip_install("numpy", "scipy", "gensim")
)


app = modal.App("glove-twitter-example")
vol = modal.Volume.from_name("my-data", create_if_missing=True)

@app.function(cpu=2, memory=4096, image=image, volumes={"/data": vol})
def use_glove():
    import gensim.downloader as api
    import re
    from gensim.models import KeyedVectors
    import os
    import unicodedata

    # Path to store/load cached model
    model_path = "/data/glove-twitter-25.kv"

    if os.path.exists(model_path):
        model = KeyedVectors.load(model_path, mmap='r')
    else:
        model = api.load("glove-twitter-25")
        model.save(model_path)

    pattern = r"Like (.+?) is to (.+?), (.+?) is to\?"
    flag = ""
    text = ""

    with open("/data/chal.txt", "r") as f:
        for line in f:
            line = line.strip()
            if not line:
                continue

            match = re.match(pattern, line.strip())

            if match:
                a, b, c = match.groups()
                va = model[a]
                vb = model[b]
                vc = model[c]

            try:
                vd = vc + (vb - va)
                result = model.similar_by_vector(vd, topn=1)[0][0]
                text += "Like " + a + " is to " + b + ", " + c + " is to " + result + "\n"
                flag += result
            except KeyError as e:
                print("Word not in vocab:", e)

    flag = unicodedata.normalize("NFKC", flag)

    print("\n Analogies: ", text)
    print("\n Flag: ",flag)
```

So what I've learned:
- At first I was using this function:
	- `result = model.most_similar(positive=[b, c], negative=[a], topn=1)[0][0]`
	So it's bad to this because it doesn't always abide with the formula `vd = vc + (vb - va)`. Like `(vb - va)` isn't always represented that way. So it's better to calculate it ourselves and then find the word representation for that vector.

