
This project contains two datasets one generated with chatito v1.0.7 and the other with v1.1.0 to test how well RasaNlu successfully learns synonim words when we provide the alias as the parsed argument in the training dataset.

### Setup

Follow the rasa setup instructions with spacy backend.

Download the required spacy models (37.4MB and 852.3MB respectively):

```
python -m spacy download en
python -m spacy download en_core_web_lg 

```

To train and run the server, you need to run this command from chatito1 or chatito2 directory.

### How to train

```
python -m rasa_nlu.train -c config_spacy.json

```

### Run server

```
python -m rasa_nlu.server -c config_spacy.json

```

### Test server request:

```
curl -XPOST localhost:5000/parse -d '{"q": "bot find places at ny"}' | python -mjson.tool

```

### DSL definition
The DSL definition used to generate the two datasets is very simple (only one intention and one argument) but is good enough for this simple test case.

```
%[findByCityAndCategory]
    ~[greet]? ~[botName]? ~[please]? ~[find]? ~[restaurants]? ~[nearby] @[city]

~[greet]
    hey
    hi
    hello
    greetings

~[botName]
    Fred
    Fredy
    Frederick

~[please]
    please
    pls

~[find]
    find
    search
    lookup

~[nearby]
    close to
    in the area of
    within
    located at
    nearby

~[restaurants]
    restaurants
    places to eat
    where to eat

~[newYork]
    new york
    ny
    new york city
    ny city

~[sanFrancisco]
    san francisco
    san francisco city

~[atlanta]
    atlanta
    atlanta city

@[city]
    ~[newYork]
    ~[sanFrancisco]
    ~[atlanta]
```
