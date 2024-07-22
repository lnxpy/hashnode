---
title: "Sighted - Read Faster, Comprehend Better With AI!"
datePublished: Mon Jul 22 2024 12:31:56 GMT+0000 (Coordinated Universal Time)
cuid: clywyv058000409lcehiv6syc
slug: sighted-read-faster-comprehend-better-with-ai
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1721404415261/18f56e42-3b8d-486e-abeb-6473d3166c80.png
tags: hackathon, ai, python, opensource, reactjs, nlp, ai-tools, nlp-transformers, aifortomorrow, bionic

---

**Highly recommended article for individuals with ADHD (Attention Deficit Hyperactivity Disorder) and Dyslexia.**

* [Sighted is LIVE here!](https://sighted.vercel.app)
    

Distraction. A very familiar term in recent decades. The Internet has been a blessing for humanity, but it has also caused several issues. When was the last time you managed to finish a book? How did it go? Have you noticed any difference between reading today and reading in 2000? How engrossed in a book are you today compared to before?

In this article, we'll introduce an AI-powered solution to improve reading quality. This is not just a basic introduction or a project demo. I'll guide you through all the decision-making phases I went through during the development of this project.

### Problem

I had ADHD as a child. My parents always said that there was nothing I could do without rushing. I was like Road Runner (the animation). 😅

Almost all of those behaviors disappeared as I grew up. However, one habit that remains is my inability to stick with books for a reasonable amount of time.

I read a paragraph, then take a break. I get back to it for a few minutes, take another break, and continue this way. Although my every smart device is on DND (Do Not Disturb) mode. I did some research and observed myself in different situations.

I realized that I needed to change myself first, but I had already tried that many times. It didn't seem to work. So, I thought, what if I change the subject? What if I modify the book to make it easier to follow, understand, and finish more quickly?

Then I came up with a concept called "Focus Reading" or "Bionic Reading".

### Bionic Reading

Bionic solutions use technology inspired by nature to solve problems. Bionic Reading is one such method, designed to help people read more efficiently. It highlights parts of the text, making it easier for the eyes to follow and understand. By emphasizing key elements, Bionic Reading helps readers process information faster, reducing cognitive load and improving reading speed. This technique benefits those with attention difficulties and anyone wanting to enhance their reading skills and retention.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721653855199/e809af6c-88d6-445f-8d88-3d3d5f58d8fd.png align="center")

### Usage

Sighted is available as an installable Python package. I designed it to be reusable and easy to install on various instances, making it compatible with front-end frameworks like React and Vue. This approach allows you to use Sighted even on language learning platforms.

#### Installation

Make sure you have `pip` and `python>=3.8` installed on your computer or instance, then run the following command.

```bash
pip install sighted
```

Sighted comes with a ~12MB pre-trained very efficient model. It's built into the library, so you won't need to download anything extra.

#### Usage

Create a Python file where we will import the necessary classes and functions.

```python
from sighted import Literal
from sighted.language import PoS

from string import Template
```

We're using the `Literal` approach for transforming. Let's create an object.

```python
text = "Hello there. This is an experimental text to showcase \
        how fast you can read with Sighted."

language = Literal(
    text=text, 
    fixation=2,
)
```

I've defined my `text` and created the `language` object, which will be transformed using the pattern I will specify later. Sighted analyzes every character, glyph, and symbol in the given text and applies the chosen pattern to it.

If you want to ignore certain parts of speech in the text, use the `PoS` enum, which includes almost all necessary parts of speech. In our example, I'm going to ignore all punctuation marks (**period, comma, apostrophe, quotation, question mark, exclamation mark, brackets, braces, parentheses, dash, hyphen, ellipsis, colon, and semicolon**).

```python
language = Literal(
    text=text, 
    fixation=2,
    ignore_pos=[PoS.PUNCT]   #  <-- new
)
```

I'll discuss `saccade` and `fixation` later, but for now, let's focus on the transformation process.

```python
transformed_text = language.transform(
    template=Template(' <span class="$pos" id="$dep"><b>$fix</b>$unfix</span>')
)
```

I'm using the native `string.Template` for template definition because Sighted can safely insert information into it. For each word in my text, I'm transforming it into a `<span />` HTML tag.

* `$fix` : The fixed (bold) part of the word.
    
* `$unfix` : The part of the text that shouldn't be bolded.
    
* `$pos` : Part of speech of the word in the text.
    
* `$dep` : Syntactic dependency of the word in the text.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721647312740/4d47fd60-c66f-4888-9603-3d618542f62d.png align="center")

The `transformed_text` is an iterable object. If I loop over it and print what it contains, I'll get this result.

```xml
<span class="intj" id="ROOT"><b>He</b>llo</span>
<span class="adv" id="advmod"><b>th</b>ere</span>
. <!-- Look how this punctuation is ignored -->
<span class="pron" id="nsubj"><b>Th</b>is</span>
<span class="aux" id="ROOT"><b>i</b>s</span>
<span class="det" id="det"><b>a</b>n</span>
<span class="adj" id="amod"><b>exper</b>imental</span>
<span class="noun" id="attr"><b>te</b>xt</span>
<span class="part" id="aux"><b>t</b>o</span>
<span class="verb" id="relcl"><b>show</b>case</span>
<span class="space" id="dep"><b>    </b>    </span>
<span class="sconj" id="advmod"><b>ho</b>w</span>
<span class="adv" id="advmod"><b>fa</b>st</span>
<span class="pron" id="nsubj"><b>yo</b>u</span>
<span class="aux" id="aux"><b>ca</b>n</span>
<span class="verb" id="ccomp"><b>re</b>ad</span>
<span class="adp" id="prep"><b>wi</b>th</span>
<span class="propn" id="pobj"><b>Sig</b>hted</span>
. <!-- Look how this punctuation is ignored -->
```

Notice the `class` attributes as well as all the IDs. If I place this result within a `<p />` tag inside a very basic HTML structure, you'll get something like this.

![Basic result](https://github.com/lnxpy/sighted/raw/main/media/img1.png align="left")

#### Styling

With a little bit of styling, you can have control over each and all parts of speech and dependencies in your text.

```css
/* unfixed letters */
p { color: gray; }

/* fixed letters */
b { color: black; }

/* adverbs */
.adv { border-bottom: solid 1px; }

/* pronouns */
.pron { color: red; }
.pron > b { color: purple; }

/* verbs */
.verb {
    background-color: yellow;
    padding: 3px;
    border-radius: 2px;
}
```

![Styled result](https://github.com/lnxpy/sighted/raw/main/media/img2.png align="left")

#### Terminal usage

It's not just about HTML. You can use any template as the input for the transformer function. See how I've used this feature to display bionic outputs in my terminal!

```python
from string import Template

from rich.console import Console
from rich.markdown import Markdown

from sighted import Literal
from sighted.language import PoS

console = Console()
text = "Hello there. This is an experimental text to showcase how fast you can read with Sighted."

language = Literal(
    text=text,
    fixation=2,
    ignore_pos=[PoS.PUNCT],
)

template = Template(" **$fix**$unfix")
transformed_text = language.transform(template)

md = Markdown("".join(list(transformed_text)))

console.print(md, style="white dim")
```

![Sighted in terminal](https://cdn.hashnode.com/res/hashnode/image/upload/v1721648522685/b9613ee9-d87e-4377-86c1-8024f317df4e.png align="center")

### Fixation & Saccade

This parameter indicates how many letters from the beginning of each word should be considered as fixation (`$fix`). It's a value between 1 to 5. As you increase it, you see that the amount of fixed letters will increase from the beginning of each word.

![Fixation differences](https://github.com/lnxpy/sighted/raw/main/media/img3.png align="left")

As I mentioned, I needed to determine the fixation formula. For each word length, I selected ten words and examined the fixation on them. Each fixation value should correspond to any word length.

$$L = \begin{cases} 1 & \text{if } W = 2 \text{ or } W < 2 \\ \min\left(\left\lceil \frac{W \cdot F}{5} \right\rceil, W\right) & \text{if } W \geq 3 \end{cases}$$

For words with a length of one or two, only the first letter is bolded. For words longer than three letters, the bottom equation will be considered.

Saccades are rapid, involuntary eye movements that play a crucial role in reading by allowing the eyes to jump quickly from one word or section of text to another.

![Eye tracking and saccade](https://github.com/lnxpy/sighted/raw/main/media/img5.png align="left")

This attribute reduces the cognitive load on the brain by making it easier to recognize and process words, thereby improving reading speed and comprehension.

![Saccade differences](https://github.com/lnxpy/sighted/raw/main/media/img4.png align="left")

If you want to know more about saccade, I highly recommend watching [this video on YouTube](https://www.youtube.com/watch?v=VFIZDZwdf-0).

### Sighted Helps with ADHD & **Dyslexia**

By presenting the text with one highly styled word at a chunk of space and controlled saccade and fixation, Sighted helps reduce visual distractions and improves focus.

* Improved focus and attention: By controlling the pace at which text is bolded, Sighted helps individuals with ADHD maintain focus and avoid distractions.
    
* Reduced visual stress: The controlled presentation of text reduces the visual overload experienced by individuals with Dyslexia, making it easier for them to process and comprehend information.
    
* Enhanced reading comprehension: It can help individuals with Dyslexia and ADHD improve their reading speed and comprehension by minimizing cognitive load and maximizing text accessibility.
    

### Development Process

This section covers the decisions I made during the development of this project. I don't see myself as a nerd, but I hope this gives you a clear idea of the process.

#### Day 1 - Starting

I discovered that social media has caused teens, including myself, to lose their connection with books. This might be due to the problems social media caused us. So, I came up with the idea.

* Researching the idea, use cases, and similar projects.
    
* Finding out, how it can solve a problem and who can benefit from it.
    
* Thinking about the possible ways that the idea can be delivered.
    
* How useful the idea is going to be. Is it even implementable?!
    

#### Day 2 - Researching

I was already familiar with tokenization, literal processing, and literature to some extent. I knew some frameworks and libraries, so diving deeper into this process wasn't a big deal for me. Instead, I focused on the tools and explored how they could benefit me.

* Learned about some keywords in this specific field.
    
    * Learned about terms like fixation, saccade, lemmatization, eye tracking, and how the human brain processes text. I also worked on a formula that calculates the fixation for each word based on its importance in the context of the sentence.
        

#### Day 3 - Feedback

Well, I couldn't rely solely on my own thoughts as a customer since I won't be the only user of this service. So, I made some parts public and shared a short teaser on socials to gauge the crowd's interest. Turned out they loved it so I kept developing.

I also tried the same technique on RTL and cursive-written languages, but it was not as effective as in English.

* Deployed a very basic MVP and asked some friends for feedback.
    
* Shared a teaser clip on socials to see the people's reaction.
    

#### Day 4 - Branding

Branding matters, especially for my idea, which was going to be a Python package, a website, and a repository. It needed to be unique. I asked ChatGPT for some help and ultimately chose "Sighted" because it comes from "Sight" which is a fitting word in the world of biology.

* Choosing a brand name, slogan, logo design, and theming.
    

#### Day 5 - Deployment 🎉

Last but not least, I hit the big green button to deploy everything on the cloud. There were a few minor issues to fix, but nothing too serious. I made it through.

Hopefully, this section has given you a clear understanding of what a hackathon submission journey may look like!

### Tech Stacks

For the website, I used **React (TypeScript)** with **Aceternity UI** and **Shadcn UI** for the UI part deployed on **Vercel**.

I used **Python** and **SpaCy** for the package development.

### Useful Links

* Website -&gt; [https://sighted.vercel.app](https://sighted.vercel.app)
    
* Website repo on GitHub -&gt; [https://github.com/lnxpy/sighted-web](https://github.com/lnxpy/sighted-web)
    
* Package -&gt; [https://pypi.org/project/sighted](https://pypi.org/project/sighted)
    
* Package repo on GitHub -&gt; [https://github.com/lnxpy/sighted](https://github.com/lnxpy/sighted)
    

### Hashnode + Bionic Reading

What if Hashnode could publish articles in bionic mode? Let me know what you think about this cool effective feature!

![Using Sighted on Hashnode blogs](https://cdn.hashnode.com/res/hashnode/image/upload/v1721592018795/83aa44e3-3f89-41ab-9c91-ca920308518a.png align="center")

### Conclusion

In conclusion, bionic technology offers a groundbreaking solution for individuals struggling with reading difficulties. By harnessing the power of bionic reading with AI (NLP), these individuals can access a more efficient and accessible means of consuming written content. The future of bionic reading holds significant promise in revolutionizing how we interact with written text, offering a beacon of hope for those seeking a more enriching and fulfilling reading experience.