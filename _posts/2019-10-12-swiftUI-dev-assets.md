---
layout: post
title: "Development Assets: How to ship applications without mock assets used for Xcode Previews."
tags:
  - Swift Evolution
  - SwiftUI
hero: https://dreamcraft.io/assets/img/whiteRectangle.png
overlay: orange
published: true
---

When we work with  [**Xcode Previews**](https://dreamcraft.io/posts/swiftui-xcode-previews), we use placeholder data(like Strings) to populate our views. But for images, the story is a little bit more complicated.
{: .lead}
<!–-break-–>
Yes, I could add an asset that's a placeholder asset for use in my previews. But that would mean that I would have to ship this asset with my application to my customers, which is not what we may want to do.
Xcode 11 has a new feature called "Development Assets" that's going to help us with this.
    

Open the **Project Editor**, and under **Targets** in general, scroll down to **Development Assets**.
<img src="https://dreamcraft.io/assets/img/devAssets/devAssets.png" style="width: 25%; height: 25%"/>​
You will notice that I already pre-configured Preview Assets as a catalog here, which will hold my 8Bit image.
<img src="https://dreamcraft.io/assets/img/devAssets/privewAssets.png" style="width: 25%; height: 25%"/>​
If you are starting from scratch and you are using one of our new templates, this will come pre-configured for you. But if you are working on an existing application, you can easily add this here.
