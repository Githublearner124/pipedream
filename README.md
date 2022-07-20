# pipedream
Pipedream_Github
print("Hello, World!")from pipedream.script_helpers import (steps, export)

# Reference data from previous steps
print(steps["trigger"]["context"]["id"])

# Return data for use in future steps
export("foo", {"test":True})from pipedream.script_helpers import export
import requests

r = requests.get("https://pokeapi.co/api/v2/pokemon/charizard")

# Return the data for use in future steps
export("data", r.json())from pipedream.script_helpers import export
import pendulum

now = pendulum.now("Etc/UTC")

# Return the data for use in future steps
export("iso_8601", now.to_iso8601_string())
export("two_days_from_now", now.add(days=2).to_datetime_string())from pipedream.script_helpers import export
import pandas as pd

d = {'col1': [1, 2], 'col2': [3, 4]}
df = pd.DataFrame(data=d)

# Return the data for use in future steps
export("df", df.to_dict())from pipedream.script_helpers import export
import numpy as np

l = np.array([2, 3, 4])

# Return the data for use in future steps
export("list", l.tolist())import os
from pipedream.script_helpers import export
import nltk
from nltk.sentiment.vader import SentimentIntensityAnalyzer

# We need to download data for our sentiment analyzer separately
# See https://www.nltk.org/data.html
# We have full access to /tmp, so we can store it there
path = "/tmp/data"
if not os.path.isdir(path):
    os.mkdir(path)
nltk.data.path.append(path)
nltk.download('vader_lexicon', download_dir=path)

# See https://www.nltk.org/howto/sentiment.html
sid = SentimentIntensityAnalyzer()
sentence = "Pipedream is awesome!"
ss = sid.polarity_scores(sentence)

# Return the data for use in future steps
export("sentence", sentence)
export("sentiment", ss)
