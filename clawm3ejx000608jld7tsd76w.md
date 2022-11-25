# Comments Make Your Code Unreadable!

Have you ever thought about the colors that your IDEs reserve for the code comments? They're mostly in soulless and dead colors like grey or dark green by default but why?! Aren't they important?! Since they're part of the codebase we maintain and ship, we can't leave them unconsidered.

This article is more theoretical than technical. The theory behind commenting. This is the main topic we will discuss throughout this article.

### Theory
Let's start with two popular concepts. Data and redundancy. Some data include meta-data in them. Redundancy is the extra clues and information hidden behind the data that allows the meaning to be understood even if the message is garbled. For instance, when someone tells you the word "Twitter" it might bring up other names such as "Elon Musk", "Followers", and "Tweet" keywords in your mind. In this case, Twitter is the data and other names are the meta-data hidden inside "Twitter".

> J-st t-y t- r--d th-s s-nt-nc-. The previous sentence was extremely garbled; all the vowels in the message were removed. However, it was still easy to decipher it and extract its meaning. (*Decoding the Universe* by [Charles Seife](https://en.wikipedia.org/wiki/Charles_Seife))

Check the following names. Even though they're so descriptive as they can explain what they do, try guessing their functionalities and what they do first.

- `isAccepted(request)`
- `isEligibleForFullFund(student)`
- `to_hex(rgb)`

As you read along, your brain eventually starts struggling to understand the hidden meta-data inside each name. It's trying to convert the keywords into phrases so that you can understand them better. Let's see how a normal problem-solving mind would understand them.

- The `isAccepted` method/function *looks* to be checking if a request is accepted.
- Same thing with `isEligibleForFullFund`. It takes the `student` and checks if he is eligible for a full-fund offer.
- The `to_hex` method/function *must be* taking an RGB value and converting that into a hex value.

Since both `isEligibleForFullFund` and `isAccepted` names start with "is", by calling them, I suppose them to return a Boolean value as well. Just like "to be" questions.

- Is she driving? Yes. (True)
- Was he writing the book? Nope. (False)

As a code reviewer, when I arrive at the line that defines the `isAccepted()` method (2nd line), I guess the method's body to be like a pseudo-structure that I quickly design in my mind (3rd-6th lines):

```python
1 |    ...
2 |    def isAccepted(request: Request) -> bool:
3 |       if ... :
4 |          return True
5 |       else:
6 |            return False
```

The pseudo-structure that came into my mind was made by the redundant information behind the `def isAccepted(request: Request) -> bool:` phrase. That's the redundancy theory behind the names. I just read its name and it told me almost %70 of its functionality and I could even guess its body. After reading its name, then I'm more acknowledged and can understand its real body from a better point of view.

Now, imagine the method's name was `checkAcceptance(request)` other than `isAccepted(request)`. There is less meta-data hidden behind the name now. I can't even guess its body. Then I see that the author has written a few lines of comments explaining what his function is doing.

```python
1 | # It takes an instance of Request class
2 | # then based on the request headers, checks
3 | # whether it is a valid request or not
4 | def checkAcceptance(request: Request) -> bool:
5 |     ...
```



### What Do We Maintain?! Source Codes or Comments?
You have probably experienced reviewing a source code that is more look to be a diary than a functional source code file like a module that contains one hundred lines of comments that explain the functionality of a ten-line function within itself! (90 lines of comments + 10 functional lines) What caused those comments to be there? Are we supposed to maintain that ten-line source code or ninety-line comment?! That's true. The weak quality of the function!

That function was not able to explain itself so the author had to write comments to explain what that function does.

> I always read the source code with the mindset that there was some logic behind the code that its author was unable to explain in the syntax so he decided to explain that in his native language. Accordingly, he's covering his failure with the help of comments since he could use a better name for his function. Right?!

### Back to the Editors
**- Why would a text editor reserve a soulless color for the highest-level bilingual language that you natively speak and write within your source codes?!**

Imagine you're commenting about the logic behind your `class` that you can't describe within your code for some reason. Isn't it better for me to see the comments in red color since the comments lead me directly to the point? So that red color will get my attention first and I'll read the comments. Now, I can read the body of the `class` from a better point of view. Of course, it saves me time.

In another word, there must've been something critical that the author decided to contact to the reviewer directly right?

Well, you might be right! We're not shipping comments. We're shipping codes. That's right. Comments are not what we maintain! We're supposed to maintain and develop the code, not the comment explaining the code! Right?! Hmm.. we'll see.

### Comments Are Failures
Believe it or not, comments are failures! Every single use of a comment represents a failure in your code. Not all of them are pure good. They're time-saving in some cases though. Your code has to be **self-descriptive** like a piece of poem. A masterpiece that its readers are pleased and graceful by reading it. Additionally, now we know that not all of them are failures! Some of them might save so much time for a code reviewer!

### Self-descriptive Code
It's all about the structure you observe for your service or product. You have to use a structure that has the ability to describe itself. Therefore, the reader/reviewer (probably a member of the team) won't need weeks or months to understand the codebase!

Example of bad practice:
```python
# Check if the employee is eligible for full benefits
if (employee.flags and HOURLY_FLAG > 0) and employee.age > 65:
    ...
```

A self-descriptive codebase won't need any use of useless comments. That's because your code is explaining itself via proper naming conventions, proper scope designs, etc.

Example of good practice:
```python
if employee.isEligibleForFullBenefits():
    ...
```

### When Not to Comment
Let's talk about the cases you better avoid writing comments or even turning things into comments. Let me get straight to the point.

- _**Don't write a comment that**_ lies!
- _**Don't write a comment that**_ shows your tasks. (TODOs)
- _**Don't write a comment that**_ covers the messes you've made.
- _**Don't write a comment that**_ is pure code!

Let's describe each bullet-list item in more detail so you won't comment improperly ever!

### A Comment That Lies
Before we dive through, a comment is lying when its context is not true. It happens when you're commenting about the functionality of a component from another file so when the functionality of that component changes based on the new requirements, you will probably not be aware of that comment's existence since it's in another file and that comment becomes a lier comment.

To solve this issue, write the comment/description where it belongs to. That way you will have all the descriptions in hand when updating an entity.

### Don’t Comment It; Clean It
I've seen some developers, commenting out the functional source codes. Either remove it or clean it. There is no room for this kind of comment in my opinion. It's not only useless, it does not make any sense to a code reviewer. Why would it be there? Is there any critical logic behind that? If so, either turn it into a new sprint task for further development or remove it all and don't check it in your VCS.

Don't let useless codes find their way into your VCS. They're worthless than being in your codebase history.

### Don’t Check In TODOs
ToDo comments have been so popular lately. I use them as well. I use some extensions and plugins to extract them all from my codebase and check them each by each when the `git commit` time arrives. Remember, you're working on a codebase. You're not supposed to maintain your ToDos in spite, they must be managed not tracked. That's why we have separated agility apps.

To solve this issue, make sure you don't check any of the ToDo comments in. Either complete them before the commit time or delete them from your codebase and keep the history clean.

### Comments Are Not Documents
We've been talking about the comments so far. Their attributes, pros, and cons. There is a huge difference between documentation/docstrings and comments as in some cases, your team may ask you to document the components you develop or even update them once in a while.

The **documentation** describes the functionality of a component and is meant to be written in a way that is understandable for the developers. However, a **comment** looks a bit personal. A piece of information about something to shape the reviewer's point of view about something (component).

### Comments and Design Patterns
Long story short, in some design patterns, you're forced to use some specific conventions. That's ok to use comments for clarification.

### Time-saving Comments
There are some cases in which I would rather see a comment regarding a component like a function that takes a piece of data and applies a RegEx pattern then returns back the results. It not only saves me time but also shows me what it expects its argument to contain. That's nice!

```python
# matches (XXX) XXX-XXXX and XXX-XXX-XXXX patterns
def hasPhoneNumber(letter) -> bool:
    return regex.search('/\b((\(\d{three}\))|\d{three}[-. ])\d{three}[-. ]\d{four}\b/;', letter)
```

### Final Words
I admired Uncle Bob's quotes and the talks he had in the Netherlands. Here you read my personal point of view about commenting. You've reached the end. Please let me know your thoughts on each section. That's always awesome knowing your thoughts on my writings.