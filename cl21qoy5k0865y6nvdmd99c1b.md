# Dynamic Contents on GitHub README

One of the coolest GitHub Actions abilities is to run a CI task to do some operations to repositories. For example, you can show the weather status on your project's readme and schedule the execution time. Eventually, you can step way further with help of this amazing tool. In this article, we are going to first, learn some basics and find a perspective about Actions and then, do some magic.

### GitHub Actions
This platform allows developers and maintainers to run CI/CD tasks and develop their products easier with less pain. [Read more about this tool](https://imsadra.me/lights-camera-github-actions).

### `git push` Action
[There is an action out there](https://github.com/ad-m/github-push-action) to push back commits to the same repository that our workflows are running on. This means we can do some stuff and push back the results to the repository. Notice that this action is not an official action represented by GitHub Inc. 

### Access Outside
Use capable technologies like Python, JS, PHP, and more to simply reach your responses. Once you got the proper shaped data, you're ready to commit.

In our case, when it comes to *capablity*, your desired tech/language should be able to work with Regular Expressions, make HTTP requests, and serialize response data like JSON and XML. Therefore, we can create a simple script in Python to access any endpoints.

### Markdown Syntax
Since we make changes to the README file, we need to know the basics of Markdown. At least, we are about to learn how to make a link section in our readme.

```markdown
[text](url)
```

### Let's Do Some Magic
Before we step through, let's discover the steps. We need a script to access outside nodes. It could be a REST service that shows our posts and we want them to be listed in our readme file as follows.

```markdown
- [title post 1](line_to_post)
- [title post 2](line_to_post)
- [title post 3](line_to_post)
```

Guess what. We got the endpoint. The following endpoint returns the last three posts from our weblog in JSON.

```json
HTTP 200 OK
Allow: GET, POST, HEAD, OPTIONS
Content-Type: application/json
Vary: Accept
URL: somewhere.com/api/v1/posts/

[
    {
        "title": "How to Use DRF",
        "slug": "how-to-use-drf",
        "draft": false,
        "authod": "Sadra"
    },
    {
        "title": "Amazing Persian Proverbs",
        "slug": "persian-proverbs",
        "draft": false,
        "author": "Sadra"
    },
    {
        "title": "OOP in Python",
        "slug": "python-oop",
        "draft": false,
        "author": "Sadra"
    }
]
```

And users can access each post if they use the `slug` field from each record in the `somewhere.com/<slug>` which means, if someone browses the following URLs, they can read the articles.

- `somewhere.com/how-to-use-drf`
- `somewhere.com/persian-proverbs`
- `somewhere.com/python-oop`

Finally, we need a script to get those data and convert them to a Markdown-like section like this. (We keep it in `result` variable)

```markdown
### My Latest Blog Posts
- [How to Use DRF](somewhere.com/how-to-use-drf)
- [Amazing Persian Proverbs](somewhere.com/persian-proverbs)
- [OOP in Python](somewhere.com/python-oop)
```

Since the push-and-commit operation will be done by action, we need to map the `result` somewhere in the readme file. Simply add a comment tag in your readme file so then the Python script uses RegEx to overwrite the `result` within the comments sections.

```markdown
### My Latest Blog Posts
<!--posts:start-->
<!--posts:end-->
```

### Python Script
Our Python script does some routine steps. Reads from an endpoint. Takes the titles and URLs and defines the `result` variable. Finally, it reads the `README.md` file and replaces the `result` variable with the *new-line* sequence within the HTML comments.

![download.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650105797775/zS9P86pKD.png)

### Use RESTful Post Feed
You can easily use my project [RESTful Post Feed](https://github.com/lnxpy/restful-post-feed), to show your latest posts from your RESTful endpoint on the readme files. All you need is to follow the steps and do some configuration. There is also [a repository](https://github.com/lnxpy/test-feed) that uses this project for more information in depth.

### Conclusion
Hopefully, this article helped you find a proper POV about the dynamic contents that maintainers can have on their readme files. A repository readme file is supposed to be a static template that gives some information about the product or there might be an introduction about someone. Now, you know the way you can make them semi-dynamic.