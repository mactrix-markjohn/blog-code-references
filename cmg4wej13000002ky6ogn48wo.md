---
title: "How to create Image target in ARFoundation similar to Vuforia engine — edit experiences visually…"
datePublished: Mon Sep 29 2025 09:00:17 GMT+0000 (Coordinated Universal Time)
cuid: cmg4wej13000002ky6ogn48wo
slug: how-to-create-image-target-in-arfoundation-similar-to-vuforia-engine-edit-experiences-visually-4951669a3742
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1758572078064/989988c3-0ff2-462c-93ba-f1a72365b039.png
tags: image-processing, foundation, augmented-reality, unity3d

---

One of the significant reasons AR developers use the Vuforia engine for Image tracking AR is simply because Vuforia allows developers to edit their experience visually on the Image reference or image target. This simple feature makes it extremely easy to create any Image tracking AR experience you can think of and also allows you to implement it perfectly.

I find ARFoundation to be easy and flexible to use compared to Vuforia. But ARFoundation seems to be limiting when developing Image Tracking AR experiences because it lacks those extra visualization features that Vuforia has.

In this article, I will show you how you can manage virtual content visually in ARFoundation similar to what Vuforia does with its image target.

### Steps to Create a “Vuforia style” Image target in ARFoundation

This process involves a lot of manipulation on AR Object Prefab to be spawned when the reference image is detected.

We will start the steps with the usual way to set up Image tracking using ARFoundation which is firstly the Reference Image Library.

#### 1\. Create the Reference Image Library

This is very easy to create. Simply right-click then go to **Create &gt; XR &gt; Reference Image Library.**

Add your Image to the Reference Image Library, you should have something like this below;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758572058496/a5112642-39d5-4f15-a5f6-ae107790a370.png align="left")

Reference Image Library

Make sure to enable **“Specify size”** it is very important for the performance of the image tracking.

The next thing to do is to enter **“0.1”** to the **X** input-field of **Physical Size (meter)**, this is also very important.

Do not worry much about the value in the **Y** input field, which will automatically populate based on pixel or Texture size.

This next part is very important, make sure to take note of the Physical Size (meters) which are **X — “0.1"** and **Y — “0.06339669"**. These numbers are important when you are creating your Object Prefab game object that will be spawned when the reference image is detected.

#### 2\. Design your AR Object Prefab

This is the most important part of this article. Whenever you are creating your object prefab for your image reference, the first thing to do is to try to reconstruct your image reference as it appears in the real world.

My Image reference is an ATM card that looks like this in the real world

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758572060325/95de63e2-941f-472a-ba26-dcad44e40afe.png align="left")

Image of my physical image reference

My goal here is to have a Gameobject replica of my ATM card in Unity which looks like this. Note that the below object was made with a Cube gameobject.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758572062240/3ce1e41d-9ee6-4577-90d7-d9edb7592801.png align="left")

A Cube gameobject with shader base image of my Image reference

Remember when setting up your Reference Image Library above, I told you to take note of the Physical size(meter) values for X and Y. Those numbers are useful now to scale the Cube gameobject.

**a. Create a Cube gameobject**

Go to your scene right-click then go to **3D object &gt; Cube**. Under the component, **Transform &gt; Scale** enter the values of your **Image reference Physical Size X and Y** to the **Scale of the Cube X and Z** input field.

Remember that our Image reference Physical Size values are 0.1 and 0.06339669 for the X and Y. These numbers should be entered into the Scale X and Z input field of the Cube, then the Y input field should be something like 0.001.

Your Cube gameobject should have the Scale value of X — 0.1, Y — 0.001, Z — 0.06339669.

(**Note:** Please ignore the Scale value in the image below which are **X: 0.083 and Z: 0.053**, it is still correct because it follows the Pixel ratio of the Image reference, but it is advisable to use **X: 0.1 and Z: 0.06339669** for consistency)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758572064266/9d5e2f47-0932-448a-9176-6ec1b6759be5.png align="left")

Cube gameobject Scale

**b. Create a Material for the Cube**

Create a material for the cube and add the image reference to the shader base color or albedo.

The purpose of this is to find out the rotation of the Cube concerning the Image reference. From my experience, I found out that the Cube gameobject is usually inverted and facing downward.

Once you determine the rotation of the Cube gameobject, simply create an **Empty Gameobject** in the Cube gameobject and enter 180 to the Y input field of the Rotation under the Transform component.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758572065788/9ed2e237-f198-47c8-9b7f-65569699009a.png align="left")

Rotation of the Empty Gameobject

This will ensure that every AR experience you are creating has the correct rotation with the real-world Image reference.

Next, remove the base image from the shader or make the shader Transparent. This will make the AR experience presentable because you do not want an inverted image to be spawned when your reference image is detected.

**c. Create a Vuforia-like Image Target for visualization**

You want to have something like the image below to let you know where to place your virtual object on the reference image to create a more dynamic and expressive AR experience.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758572066558/6ac1ed21-a542-4302-9029-6172da23b4e4.png align="left")

You can duplicate your parent Cube gameobject and drag it into the Empty gameobject you just rotated by 180 or you can just create a new Cube gameobject inside the Empty gameobject and assign it the same Scale value as the parent gameobject.

Once you get the scaling right, create a new material for the new Cube that you can rename \*\*“ImageTarget”. (\*\*From now on, we will refer to the new Cube gameobject as **“ImageTarget cube”)**.

Then add the Image reference to the Albedo or base color of the shader. Once that is done, you will have a similar gameobject as shown in the image above.

The ImageTarget cube will allow you to visually edit your experience the way you want and when you spawn it in the real world, every virtual content will be positioned as you have implemented it.

**d. Add your Virtual objects or AR experience**

Since you have successfully reconstructed your physical image reference as it appears in the real world, now you can add whatever you want, which could be a 3D model of a character, furniture, an image, a video, or animation of anything.

In the end, you want something that looks like this below;

To create this, simply add your AR experience inside the Empty gameobject you rotated by 180.

Your hierarchy should look like this;

(**Note**: The **Empty gameobject** here has been renamed as **“Content”** and the chair from the image above is named “chair-set”. The Lamp for best practice should be inside the “Content” gameobject.)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758572068134/4d5f24c0-81a9-4946-8123-a206a9421355.png align="left")

Inside the Empty gameobject

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758572069613/af2708cd-00f7-48e4-a0e5-3f7d2b54532c.png align="left")

A better example of the Content structure

**e. Deactivate the ImageTarget cube**

You should have noticed from the two images above that game objects named\*\*“CardSize”\*\* and **“ARVRAfricaTemplate”** are currently deactivated or inactive. These gameobjects are our “ImageTarget cube” created above.

The reason for this is to allow only the AR experience or virtual content to be visible once the Object Prefab is spawned once the Image reference is detected.

Once you deactivate the ImageTarget cube, your Object Prefab should look like this below;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758572070917/5438864f-5de9-451a-a0bc-28e5532c1cd4.png align="left")

Virtual content once ImageTaregt cube is deactivated

At this point, there is nothing left to do in the Object Prefab. The next step is simply to make your gameobject a prefab by dragging it into your Prefab folder.

### 3\. Assign your AR Object Prefab to your Image Tracking Script

The next step from here on is easy and it is something you are very familiar with.

Assign your new prefab to your Image tracking script that controls your ARFoundation image tracking AR experience.

You should have something similar to this below;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758572072756/6f9fbacc-19f5-45b0-821c-efb9a86bbf7d.png align="left")

The next thing to do is to tweak your code a little.

### 4\. In your code, Scale your AR Object Prefab to the scale of the TrackedImage

This next step is as important as Step 2.

In your code, once you get the TrackedImage from the event listener of ARTrackedImageManager, make sure to get the width and height of the Image reference and use that value to change the X and Z scale of your AR Object Prefab.

Your code should look like this below;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758572074221/bcf31b4c-61d1-489b-8c36-a7185868e4cc.png align="left")

Scale Object Prefab to Image Reference size

Pay close attention to the last line of the code snippet above, you will see that the scale of the AR Object Prefab was changed to this;

> arObject.transform.localScale = new Vector3(image.referenceImage.size.x,arObject.transform.localScale.y,image.referenceImage.size.y);

This is important because it will make sure that your AR Object Prefab is always the same size as your Image reference or your TrackedImage.

Remember that when we were creating our AR Object Prefab, the parent Cube gameobject had the scale X: 0.1, Y: 0.001, and Z: 0.06339669.

This scale we initially assigned to the AR Object Prefab and creating our AR experience around it, will ensure that all our AR experience or virtual contents are appropriately scaled as we initially designed it.

### 5\. Final Result

Once you are done with everything, you should have something similar to this below;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758572075819/aff55a1e-0848-41c4-9374-c9510fef4790.png align="left")

Final Result

#### Watch the YouTube video of the AR Experience

[**ARFoundation Image Tracking - Place your 3D model at any position on the Physical image**](https://youtube.com/shorts/ULjBvzMZd_Y?feature=share)

### Summary

ARFoundation for me is very easy and flexible to use, and it is quite sad that it does not have this feature in-built. But with this tutorial, you can still get a lot done and even have more flexibility on what you can do when developing an Image Tracking solution using ARFoundation.

#### PS:

If you have read this far, thank you very much for your patience. This is my first-ever tutorial on Augmented Reality development. I hope that I will be able to create more in the future.

If you want a more detailed course on this, I have created a video course to show you step by step how to implement Image tracking in Unity 3D with AR Foundation.

👉 [Check out the course here](https://sites.google.com/view/mactrixblog/landing-pages/udemy-course-ar-image-tracking)

But if you are the one who loves books, both eBook or printed book, you can check out my book titled “C# for Augmented Reality: Using Unity AR Foundation and Niantic Lightship ARDK.” More tutorials are in there [https://www.amazon.com/dp/B0C52BTHJX](https://www.amazon.com/dp/B0C52BTHJX)

[If you found value in this article](https://www.amazon.com/dp/B0C52BTHJX) and would like to support my continued work, consider contributing through Buy Me a Coffee. Your support helps sustain the time, research, and effort that go into creating quality content.  
👉 [https://buymeacoffee.com/johnokparaeke](https://buymeacoffee.com/johnokparaeke)

Thank you for reading my article, and have a wonderful day. Bye!!!!!!