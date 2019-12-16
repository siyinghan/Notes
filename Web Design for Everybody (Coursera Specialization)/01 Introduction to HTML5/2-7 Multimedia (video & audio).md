# 2-7 Multimedia (video & audio)

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/133.jpg' alt='133' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/134.jpg' alt='134' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/135.jpg' alt='135' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/136.jpg' alt='136' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/137.jpg' alt='137' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/138.jpg' alt='138' width='500px' />

`.ext#t=5, 25`: I want the music only play from 5 to 25 seconds.

`.ext#t=, 39`: Start at the beginning and only are going to play the first 39 seconds.

`.ext#t=, 1:38:45`: I want to start at one minute 38 seconds, and just go ahead and play to 45.

`.ext#t=42`: Start at the 42 second and play from there.

**Example for Video element:**
------

Video does not play automatically when the web page is opened：

```html
<h1>Video</h1>
<video src="BoxCar.MOV" widht="400">
  Your browser does not support the <code>video</code> element.
</video>
```

Video plays automatically when the web page is opened：

```html
<h1>Video</h1>
<video src="BoxCar.MOV" widht="400" autoplay>
  Your browser does not support the <code>video</code> element.
</video>
```

Video with a **control panel**:

```html
<h1>Video</h1>
<video src="BoxCar.MOV" widht="400" controls>
  Your browser does not support the <code>video</code> element.
</video>
```

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/139.png' alt='139' width='350px' />

Multiple attributes:

```html
<h1>Video</h1>
<video src="BoxCar.MOV" widht="400" controls loop>
  Your browser does not support the <code>video</code> element.
</video>
```

**Example for Audio element:**
------

```html
<h1>Audio</h1>
<audio
  src="https://upload.wikimedia.org/wikipedia/commons/0/04/Pyotr_Ilyich_Tchaikovsky_-_1812_overture.ogg"
  controls>
  Pyotr Ilyich Tchaikovsky - 1812 overture
</audio>
<br />
<audio
  src="https://upload.wikimedia.org/wikipedia/commons/0/04/Pyotr_Ilyich_Tchaikovsky_-_1812_overture.ogg#t=15:35"
  controls>
  Pyotr Ilyich Tchaikovsky - 1812 overture, but set to start at the exciting
  part!
</audio>
```



<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/140.png' alt='140' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/141.jpg' alt='141' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/142.jpg' alt='142' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/143.jpg' alt='143' width='500px' />
