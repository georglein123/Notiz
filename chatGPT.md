chatGPT

## 使用场景

1. 问答

Q&A

基于已有知识回答问题

Answer questions based on existing knowledge.

I am a highly intelligent question answering bot. If you ask me a question that is rooted in truth, I will give you the answer. If you ask me a question that is nonsense, trickery, or has no clear answer, I will respond with "Unknown". 

```
Q: How does a telescope work?
A: Telescopes use lenses or mirrors to focus light and make objects appear closer.
```



2. 修改英语语法

**Grammar correction**

Corrects sentences into standard English.

```
Correct this to standard English:

She no went to the market.
```

第三人称转换

Converts first-person POV to the third-person. This is modified from a community prompt to use fewer examples.

```
Convert this from first-person to third person (gender female):

I decided to make a movie about Ada Lovelace.
```



3. 简单总结概况

Translates difficult text into simpler concepts.

```
Summarize this for a second-grade student:

Jupiter is the fifth planet from the Sun and the largest in the Solar System. It is a gas giant with a mass one-thousandth that of the Sun, but two-and-a-half times that of all the other planets in the Solar System combined. Jupiter is one of the brightest objects visible to the naked eye in the night sky, and has been known to ancient civilizations since before recorded history. It is named after the Roman god Jupiter.[19] When viewed from Earth, Jupiter can be bright enough for its reflected light to cast visible shadows,[20] and is on average the third-brightest natural object in the night sky after the Moon and Venus.
```

文本总结分析

TLDR（too long, didn't read）

Summarize text by adding a 'tl;dr:' to the end of a text passage. It shows that the API understands how to perform a number of tasks with no instructions.

```
A neutron star is the collapsed core of a massive supergiant star, which had a total mass of between 10 and 25 solar masses, possibly more if the star was especially metal-rich.[1] Neutron stars are the smallest and densest stellar objects, excluding black holes and hypothetical white holes, quark stars, and strange stars.[2] Neutron stars have a radius on the order of 10 kilometres (6.2 mi) and a mass of about 1.4 solar masses.[3] They result from the supernova explosion of a massive star, combined with gravitational collapse, that compresses the core past white dwarf star density to that of atomic nuclei.

Tl;dr
```

简写笔记转换成总结文字

Turn meeting notes into a summary.

```
Convert my short hand into a first-hand account of the meeting:

Tom: Profits up 50%
Jane: New servers are online
Kjel: Need more time to fix software
Jane: Happy to help
Parkman: Beta testing almost done
```





4. 使用自然语言调用opanai 的api**Natural language to OpenAI API**

Create code to call to the OpenAI API using a natural language instruction.

```
"""
Util exposes the following:
util.openai() -> authenticates & returns the openai module, which has the following functions:
openai.Completion.create(
    prompt="<my prompt>", # The prompt to start completing from
    max_tokens=123, # The max number of tokens to generate
    temperature=1.0 # A measure of randomness
    echo=True, # Whether to return the prompt in addition to the generated completion
)
"""
import util
"""
Create an OpenAI completion starting from the prompt "Once upon an AI", no more than 5 tokens. Does not include the prompt.
"""
```



5. 翻译

Translates English text into French, Spanish and Japanese.

```
Translate this into 1. French, 2. Spanish and 3. Japanese:

What rooms do you have available?

```

6. （范式）文本信息结构化整理

Create tables from long form text by specifying a structure and supplying some examples.

```
A table summarizing the fruits from Goocrux:

There are many fruits that were found on the recently discovered planet Goocrux. There are neoskizzles that grow there, which are purple and taste like candy. There are also loheckles, which are a grayish blue fruit and are very tart, a little bit like a lemon. Pounits are a bright green color and are more savory than sweet. There are also plenty of loopnovas which are a neon pink flavor and taste like cotton candy. Finally, there are fruits called glowls, which have a very sour and bitter taste which is acidic and caustic, and a pale orange tinge to them.

| Fruit | Color | Flavor |
```

研究主题的框架生成

Generate an outline for a research topic.

```
Create an outline for an essay about Nikola Tesla and his contributions to technology:
```



7. （范式）分类

Classify items into categories via example.

```
The following is a list of companies and the categories they fall into:

Apple, Facebook, Fedex

Apple
Category:
```



8. python代码解读

Explain a piece of Python code in human understandable language.

```
# Python 3 
def remove_common_prefix(x, prefix, ws_prefix): 
    x["completion"] = x["completion"].str[len(prefix) :] 
    if ws_prefix: 
        # keep the single whitespace as prefix 
        x["completion"] = " " + x["completion"] 
return x 

# Explanation of what the code does

#
```



长代码解读

Explain a complicated piece of code.

```
class Log:
    def __init__(self, path):
        dirname = os.path.dirname(path)
        os.makedirs(dirname, exist_ok=True)
        f = open(path, "a+")

        # Check that the file is newline-terminated
        size = os.path.getsize(path)
        if size > 0:
            f.seek(size - 1)
            end = f.read(1)
            if end != "\n":
                f.write("\n")
        self.f = f
        self.path = path

    def log(self, event):
        event["_event_id"] = str(uuid.uuid4())
        json.dump(event, self.f)
        self.f.write("\n")

    def state(self):
        state = {"complete": set(), "last": None}
        for line in open(self.path):
            event = json.loads(line)
            if event["type"] == "submit" and event["success"]:
                state["complete"].add(event["id"])
                state["last"] = event
        return state

"""
Here's what the above class is doing:
1.
```

python代码解bug

There's a number of ways of structuring the prompt for checking for bugs. Here we add a comment suggesting that source code is buggy, and then ask codex to generate a fixed code.

```
##### Fix bugs in the below function
 
### Buggy Python
import Random
a = random.randint(1,12)
b = random.randint(1,12)
for i in range(10):
    question = "What is "+a+" x "+b+"? "
    answer = input(question)
    if answer = a*b
        print (Well done!)
    else:
        print("No.")
    
### Fixed Python
```



python docstring说明编写

An example of how to create a docstring for a given Python function. We specify the Python version, paste in the code, and then ask within a comment for a docstring, and give a characteristic beginning of a docstring (""").

```
# Python 3.7
 
def randomly_split_dataset(folder, filename, split_ratio=[0.8, 0.2]):
    df = pd.read_json(folder + filename, lines=True)
    train_name, test_name = "train.jsonl", "test.jsonl"
    df_train, df_test = train_test_split(df, test_size=split_ratio[1], random_state=42)
    df_train.to_json(folder + train_name, orient='records', lines=True)
    df_test.to_json(folder + test_name, orient='records', lines=True)
randomly_split_dataset('finetune_data/', 'dataset.jsonl')
    
# An elaborate, high quality docstring for the above function:
```



9. 电影标题emoji转换

Convert movie titles into emoji.

```
Convert movie titles into emoji.

Back to the Future: 👨👴🚗🕒 
Batman: 🤵🦇 
Transformers: 🚗🤖 
Star Wars:
```



10. 计算代码的时间复杂度

Find the time complexity of a function.

```
def foo(n, k):
accum = 0
for i in range(n):
    for l in range(k):
        accum += i
return accum
"""
The time complexity of this function is
```



11. 编程语言转换

To translate from one programming language to another we can use the comments to specify the source and target languages.

```
##### Translate this function  from Python into Haskell
### Python
    
    def predict_proba(X: Iterable[str]):
        return np.array([predict_one_probas(tweet) for tweet in X])
    
### Haskell
```



12. 情绪分辨

This is an advanced prompt for detecting sentiment. It allows you to provide it with a list of status updates and then provide a sentiment for each one.

```
Classify the sentiment in these tweets:

1. "I can't stand homework"
2. "This sucks. I'm bored 😠"
3. "I can't wait for Halloween!!!"
4. "My cat is adorable ❤️❤️"
5. "I hate chocolate"

Tweet sentiment ratings:
```



13. 提取关键字

Extract keywords from a block of text. At a lower temperature it picks keywords from the text. At a higher temperature it will generate related keywords which can be helpful for creating search indexes.

```
Extract keywords from this text:

Black-on-black ware is a 20th- and 21st-century pottery tradition developed by the Puebloan Native American ceramic artists in Northern New Mexico. Traditional reduction-fired blackware has been made for centuries by pueblo artists. Black-on-black ware of the past century is produced with a smooth surface, with the designs applied through selective burnishing or the application of refractory slip. Another style involves carving or incising designs and selectively polishing the raised areas. For generations several families from Kha'po Owingeh and P'ohwhóge Owingeh pueblos have been making black-on-black ware with the techniques passed down from matriarch potters. Artists from other pueblos have also produced black-on-black ware. Several contemporary artists have created works honoring the pottery of their ancestors.
```



14. 广告词

Turn a product description into ad copy.

```
Write a creative ad for the following product to run on Facebook aimed at parents:

Product: Learning Room is a virtual environment to help students from kindergarten to high school excel in school.
```



15. （范式）产品命名

Create product names from examples words. Influenced by a community prompt.

```
Product description: A home milkshake maker
Seed words: fast, healthy, compact.
Product names: HomeShaker, Fit Shaker, QuickShake, Shake Maker

Product description: A pair of shoes that can fit any foot size.
Seed words: adaptable, fit, omni-fit.
```



关键词联系脑暴

Create ideas for fitness and virtual reality games.

```
Brainstorm some ideas combining VR and fitness:
```



16. 创建电子表格

Create spreadsheets of various kinds of data. It's a long prompt but very versatile. Output can be copy+pasted into a text file and saved as a .csv with pipe separators.

```
A two-column spreadsheet of top science fiction movies and the year of release:

Title |  Year of release
```



17. JavaScript专家

This is a message-style chatbot that can answer questions about using JavaScript. It uses a few examples to get the conversation started.

```
You: How do I combine arrays?
JavaScript chatbot: You can use the concat() method.
You: How do you make an alert appear after 10 seconds?
JavaScript chatbot
```



JavaScript一行函数编写

Turn a JavaScript function into a one liner.

```
Use list comprehension to convert this into one line of JavaScript:

dogs.forEach((dog) => {
    car.push(dog);
});

JavaScript one line version:
```





javaScript转换成python

Convert simple JavaScript expressions into Python.

```
#JavaScript to Python:
JavaScript: 
dogs = ["bill", "joe", "carl"]
car = []
dogs.forEach((dog) {
    car.push(dog);
});

Python:
```







18. 机器学习/人工智能专家

This is a QA-style chatbot that answers questions about language models.

```
ML Tutor: I am a ML/AI language model tutor
You: What is a language model?
ML Tutor: A language model is a statistical model that describes the probability of a word given the previous words.
You: What is a statistical model?
```



19. 科幻小说清单

This makes a list of science fiction books and stops when it reaches #10.

```
List 10 science fiction books:
```



20. SQL语言编写

Create simple SQL queries.

```
Create a SQL request to find all users who live in California and have over 1000 credits:
```



21. 提取联系信息

Extract contact information from a block of text.

```
Extract the name and mailing address from this email:

Dear Kelly,

It was great to talk to you at the seminar. I thought Jane's talk was quite good.

Thank you for the book. Here's my address 2111 Ash Lane, Crestview CA 92002

Best,

Maya

Name:
```



22. 类比创建

Create analogies. Modified from a community prompt to require fewer examples.

```
Create an analogy for this phrase:

Questions are arrows in that:
```



23. 创建食谱

Create a recipe from a list of ingredients.

```
Write a recipe based on these ingredients and instructions:

Frito Pie

Ingredients:
Fritos
Chili
Shredded cheddar cheese
Sweet white or red onions, diced small
Sour cream

Instructions:
```

24. 餐厅评价

Turn a few words into a restaurant review.

```
Write a restaurant review based on these notes:

Name: The Blue Wharf
Lobster great, noisy, service polite, prices good.

Review:
```



25. 学习要点

Provide a topic and get study notes.

```
What are 5 key points I should know when studying Ancient Rome?
```



26. 面试问题

Create interview questions.

```
Create a list of 8 questions for my interview with a science fiction author:
```



## 如何提问

1. 提供一些例子指导

例如

```
Suggest three names for a horse that is a superhero.
```

换成下方这个

```
Suggest three names for an animal that is a superhero.

Animal: Cat
Names: Captain Sharpclaw, Agent Fluffball, The Incredible Feline
Animal: Dog
Names: Ruff the Protector, Wonder Canine, Sir Barks-a-Lot
Animal: Horse
Names:
```

2. 调节temperature 参数，temperature参数[0,1]，在至0以上，可以在每次提交相同问题时获得不同回答，temperature越低，回答越精确稳定，temperature越高，回答越发散







API

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