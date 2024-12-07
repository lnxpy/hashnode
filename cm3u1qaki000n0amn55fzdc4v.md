---
title: "I Switched to Hashnode Docs"
datePublished: Sat Nov 23 2024 10:47:28 GMT+0000 (Coordinated Universal Time)
cuid: cm3u1qaki000n0amn55fzdc4v
slug: i-switched-to-hashnode-docs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1732354287948/1ffa69bc-4c81-4e71-8835-6d10ff1901ec.png
tags: github, python, documentation, material, hashnode, docs, documents, mkdocs, github-actions-1, pyaction

---

A few months ago, Hashnode launched a new app called "Docs", and I decided to move the documentation of one of my open-source projects to Hashnode.

%[https://pyaction.imsadra.me/docs] 

Working with it is as simple as writing blogs on Hashnode but in an organized way. I decided to write my fresh experience of using Docs for a public open-source tool.

### I Should’ve Reconsidered My Decision

As an open-source developer, I think I should’ve reconsidered my decision when I first decided to deploy on Hashnode Docs.

#### The separation of docs and project

I’m feeling a few concerns about Hashnode Docs. The main reason is that I’m separating the documentation from my codebase and hosting it elsewhere.

It's like a double-edged sword. You can modify and deploy it very quickly, but only your team has access to the docs, and not everyone can contribute to it.

There is a "GitHub" feature that will be available soon, but I don't think it will be the same as keeping the documentation within the scope of the project itself. It seems more like a backup system for the documentation in my opinion.

#### Lack of customizability

I moved my documentation from [MkDocs Material](https://squidfunk.github.io/mkdocs-material/), which was highly customizable. It offered many plugins and extensions, and you could modify existing features, which was really nice.

I haven't seen these options on Hashnode. Remember, Hashnode Docs *isn't just for developers*. In my view, it's designed to let you document anything, regardless of the level of programming knowledge. On the other hand, tools like [MkDocs](https://www.mkdocs.org/) and [Sphinx](https://www.sphinx-doc.org/en/master/) are meant for developers who prefer to work directly in a text editor.

#### Code highlighting feature

You include many code snippets in your docs, and this is another area where Hashnode could improve. The syntax highlighting feature is somewhat lacking, as it doesn't recognize all the keywords in some languages, which can be frustrating at first. Considering the fresh modern look of (`/callout`), the code snippets could be more visually appealing. I strongly feel that code snippets haven't changed much since the first release of Hashnode, and Hashnode Docs is still using the same setup.

#### Including badges, icons, and in-line images

Including badges is another issue with Docs. I wish I could add some [Shields.io](https://shields.io/) badges to my docs to show the current status of my project.

I tried to use tables to put badges in them but you can’t put images inside the table cells. I tried buttons, although I managed to put the badges in them but the looking wasn’t too good.

#### No versioning or tagging feature

There is no recovery feature yet. If you delete any part of your document, you can't retrieve it back. Tagging and versioning in documents are very important features. Fortunately, Hashnode offers "Revision History" for blogs. I hope they add the same functionality for documents soon, perhaps with the ability to tag specific states of the docs.

#### No translation feature

If you want to translate your docs into another language, there is currently no feature available for that.

### Things I Love About Hashnode Docs

I switched to Hashnode Docs for a reason. Let's look at what really caught my attention and convinced me to move to Hashnode Docs.

#### New commands and markdown items

There are many features that help you present your docs effectively. You can use `/steps`, `/card`, `/accordion`, `/tabs`, and even `/button` to customize your docs and make the reading experience more engaging. None of these markdown items are available on blogs which makes docs more unique.

#### No more CI pipeline or deployment

You don't need a CI pipeline to deploy your documentation after each change, which allows for continuous publication—this is fantastic. Additionally, making changes to your documents is easy and straightforward.

#### SEO is the next level

In a word, Hashnode’s SEO team is outstanding. Even if you try to harm your docs' SEO, Hashnode still manages to share your docs with the world. It's amazing how powerful this is.

#### Perfect choice for open-source projects

If you're looking for a platform to publish the documentation for your open-source project, Hashnode Docs is a great choice. It includes features that read various parameters from the GitHub repository you specify, such as the number of stars your repository has.

#### Fast to navigate and engage

Its routing system is quick, letting you move instantly between pages and documents without waiting for the full page to load. Only the content section reloads.

### Final Word

Keep in mind, it's only been a few months since Hashnode Docs was released. So, many of my complaints and concerns might disappear in a few months.