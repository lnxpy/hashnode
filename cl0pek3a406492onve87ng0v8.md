## Explain Git Like I'm Five

As you've probably heard everywhere, Git is a Version Control System tool. Does it refer to `v1.0` `v2.3.23.1`? Do you have any idea about that? In this article, I aim to introduce you to this system in another aspect. **Let's see if illustrations could help us dive into this powerful mechanism**.

## Antique Sales
A company named “Shiraz” is trying to sell a valuable picture that is going to be drawn by some famous painters. All they have is a frame with a white canvas there for now. All painters have signed the contracts and waiting for the tasks. Sadra is one of them. They are all about the create a **Masterpiece**.


![Untitled2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1647181969324/cKUe6yWFs.png)

 Shiraz decides to keep the canvas publicly available for viewers while painters can contribute to the masterpiece remotely. Artists can simply request Shiraz for the last update of the artwork which is a simple printed paper of the masterpiece with the last changes applied. Painters simply make their changes and ask Shiraz for a quick update to the original artwork. Every artist has his/her special skills. Sadra is so professional at drawing clouds, lights, and shadows so then he's not going to draw any houses, trees, grass materials, and so on. He is looking at the sky wishing nothing disturb his artwork on that side of the canvas. After all contributions, now it's Sadra's turn. Meanwhile, Jeff, who's Sadra's friend, decides to draw some birds in the sky. He didn't know how important tasks priorities were so he makes a mistake. After he drew all birds in the sky, he asks for a quick update to the original artwork. Here is what people are seeing in the gallery at the moment.
 

![Untitled.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1647182089540/4sFEhSicX.png)

On the other hand, Sadra is working on the clouds. Unfortunately, Sadra doesn’t find birds that much interesting and refuses to use them in his artworks for some reason. Here is the final result drew by Sadra. (He forgot to update his artwork before he starts drawing)

![Untitled3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1647182101280/AkoTLTp4r.png)

Here we have the last updated version of the **Masterpiece** on both Shiraz and Sadra's canvases.

![Untitled4.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1647182110715/E02vTKPJ4.png)

Since Shiraz workers don't know much about painting, what happens if Sadra asks Shiraz for a quick update with his last changes? Should Shiraz choose between those two artworks?

### Birds or Clouds? That is The Question!
Once Sadra calls a Shiraz worker who's working in the updating section to ask him to update the original artwork with his last changes, they refuse the request and the reason is that there was someone who had worked on that part already which makes Sadra annoyed. The worker wants Sadra to calm down and take a deep breath. They give Sadra the last updated original artwork and Sadra is shocked by the unexpected birds. There was a sign in the contributions list that proves that Jeff did draw those birds. After a quick call to Jeff, Sadra decides to combine them together so we will have both birds and clouds in our **Masterpiece** which is so cool. Finally, Sadra retrieves the last update of the original artwork and starts working on that.

![Untitled5.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1647182198073/tSZBt-7E_.png)

Way more beautiful. Isn't it? So in this case, Sadra, Jeff, and other artists didn't use any Version Control System at all and that's why Sadra had to call the worker in order to fix the issue (**conflict**) all on his own. With tools like Git, all these operations will be well-managed and organized.

By the way, We experienced a horrible conflict. Jeff made a mistake so Sadra did too. He forgot to ask for the last changes and started drawing without the last changes applied to his personal canvas. That made him redesign his sky part. Finally, Shiraz company was able to sell the **Masterpiece** at its best price.

### Conclusion
In this article, we learned some basics of a simple Version Control System scenario. We fixed a conflict and made a **Masterpiece**. Always keep yourself updated which Sadra was not actually into it.