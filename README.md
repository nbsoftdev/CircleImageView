=========CircleImageView======


![CircleImageView](https://raw.githubusercontent.com/nbsoftdev/CircleImageView/refs/heads/master/Screenshot-1.png)![CircleImageView](https://raw.githubusercontent.com/nbsoftdev/CircleImageView/refs/heads/master/Screenshot-2.png)


[![](https://jitpack.io/v/nbsoftdev/CircleImageView.svg)](https://jitpack.io/#nbsoftdev/CircleImageView)



It uses a BitmapShader and **does not**:
* Create a copy of the original bitmap
* use a clipPath (which is neither hardware accelerated nor anti-aliased)
* use setXfermode to clip the bitmap (which means drawing twice to the canvas)

As this is just a custom ImageView and not a custom Drawable or a combination of both, it can be used with all kinds of drawables, i.e. a PicassoDrawable from [Picasso](https://github.com/square/picasso) or other non-standard drawables (needs some testing though).


Step 1. Add the JitPack repository to your build file.
Add it in your root build.gradle at the end of repositories:
------
```
dependencyResolutionManagement {
		repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
		repositories {
			mavenCentral()
			maven { url 'https://jitpack.io' }
		}
	}
 ```

Gradle
------
```
dependencies {
    ...
    implementation 'com.github.nbsoftdev:CircleImageView:$latestversion'
}
```

Usage
-----
```xml
    <com.nbsoftdev.circleimageview.CircleImageView
        android:id="@+id/profile_image"
        android:layout_width="150dp"
        android:layout_height="150dp"
        android:src="@drawable/profile"
        app:nbs_border_width="2dp"
        android:layout_centerInParent="true"
        app:nbs_border_color="#F44336" />
```

Limitations
-----------
* The ScaleType is always CENTER_CROP and you'll get an exception if you try to change it. This is (currently) by design as it's perfectly fine for profile images.
* Enabling `adjustViewBounds` is not supported as this requires an unsupported ScaleType
* If you use an image-loading library like Picasso or Glide, you need to disable their fade animations to avoid messed-up images. For Picasso use the `noFade()` option, for Glide use `dontAnimate()`. If you want to keep the fadeIn animation, you have to fetch the image into a `Target` and apply a custom animation yourself when receiving the `Bitmap`.
* Using a `TransitionDrawable` with `CircleImageView` doesn't work properly and leads to messed up images.

FAQ
---
**How can I use a `VectorDrawable` with `CircleImageView`?**

Short answer: you shouldn't. Using a `VectorDrawable` with `CircleImageView` is very inefficient. You should modify your vectors to be in a circular shape and use them with a regular ImageView instead.

**Why doesn't `CircleImageView` extend `AppCompatImageView`?**

Extending `AppCompatImageView` would require adding a runtime dependency for the support library without any real benefit.


Changelog
---------
* **1.1.0**
    * Initial release

License
-------

    Copyright 2014 - 2020 Henning Dodenhof

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
