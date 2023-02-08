# Hashnode Blog, but More Dynamic!

Here I've brought you something quite cool. What if you could pick a random header background image every time someone hops into your blog?!

Hmm.. yes. Let's do that but for now, let me show you a simple preview at each page-refresh.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1675768931274/fcc10e4e-46db-42f5-a822-ac3ec71caad6.gif align="center")

For this purpose, we're going to use the [Lorem Picsum](https://picsum.photos/) service. It generates new random images on each request call you make based on the specified query parameters. So, with a bit of coding, we can achieve that.

### Setup Process

That's quite clever if we get our hands on some examples first then we'll be able to generate awesome fit images for our header.

I had several attempts with different image sizes on different resolutions and it turned out that the best case would be choosing **2500x1200** pixels for our blog header images. Any image smaller than that might get cut off or appear blurry if it needs to fill the browser width.

#### 1\. Create the base URL

So far, our URL should look like `https://picsum.photos/2500/1200/`. If you [browse it](https://picsum.photos/2500/1200/), you'll see random images in specified width and height each time on each page-refresh.

#### 2\. Apply effects

This part is optional. In fact, you can blurify your image up to 10 levels or even render it in the grayscale color space. All you need to do is use `grayscale` and/or `blur` parameters in the following ways.

* Slightly blurred: `https://picsum.photos/2500/1200/?blur`
    
* Max blurry: `https://picsum.photos/2500/1200/?blur=10`
    
* B&W and blurred: `https://picsum.photos/2500/1200/?grayscale&blured`
    

Make sure your URL works and the image appears on your browser tab. Choosing the right parameters is all up to your header's design whether it matches blurry images or black and white. Copy the URL and get ready for some CSS work.

#### 3\. Enable "Custom CSS"

Head over to your dashboard and select the "**Appearance**" tab. Scroll all the way down and you should see the Custom CSS feature. It should be disabled by default so enable it first then hit the "**Update**" button. Finally, click "**Edit Custom Stylesheet**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1675805197583/fc7a029f-bb87-4fe3-a2ea-0034910d653d.png align="center")

#### 4\. Paste out the CSS

Switch to the "**Home**" tab if it's not switched already. Copy and paste the following CSS snippet into the editor but don't forget to change the `<IMAGE-URL>` phrase with the URL you copied earlier.

```css
.blog-header{
    background: url(<IMAGE-URL>);
    background-attachment: fixed;
    background-size: cover;
}
```

Your editor should look like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1675808763600/3c7b1c5a-f662-447a-8c82-62f671f07b35.png align="center")

Now, scroll down and hit "**Save Styles**" and finally "**Publish**" and it's done.

Head back to your weblog main page and you should see the result. If it's not appearing yet, check it out in Incognito. It might affect a few minutes later due to caching and CDN reasons.

**Note**: If you don't want the background image to be fixed while scrolling, simply comment out the third line of the above code snippet.

### This Trick Might be Expensive

Depending on the image size and the scale you specify for your image and lots of other components, it might be a costly request. Since there is no caching in this case, that might be a better choice to use a static image from Hashnode's official CDN. A good trick is that you can upload an image in one of your drafts, then look for the URL to that image and use it as your blog header's background image.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1675809162013/d160b8bd-9469-4d25-a84d-6e72877b4760.png align="center")

Thanks for following up toward the end. Hope you enjoyed this trick and could add more beauty elements to the main page of your blog although your profile avatar has already made that page quite beautiful.