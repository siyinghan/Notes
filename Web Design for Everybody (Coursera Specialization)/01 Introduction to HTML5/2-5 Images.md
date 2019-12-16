# 2-5 Images

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/103.jpg' alt='103' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/104.jpg' alt='104' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/105.jpg' alt='105' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/106.jpg' alt='106' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/107.jpg' alt='107' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/108.jpg' alt='108' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/109.jpg' alt='109' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/110.jpg' alt='110' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/111.jpg' alt='111' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/112.jpg' alt='112' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/113.jpg' alt='113' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/114.jpg' alt='114' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/115.jpg' alt='115' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/116.jpg' alt='116' width='500px' />

Creating good alternative text is almost an art. The good news is that it is an art that even artistically-challenged people like myself can do well. The key is to think about the meanings behind your images, not a description of them. So here are some tips:

## Tips 

- **Decide what information the image conveys:** Does someone need to see the page to understand your     message? If not, you can treat the image as decorative use a null (empty)     text alternative (alt=""). Make sure not to include a space     inside the quotes since some screen readers may then read it aloud.
- **If the image is information, be complete, but concise**: In most cases you should be able to use a     short phrase or sentence as alt text. 
- **Prioritize information in text alternative:** Aim to put the most important information at the     beginning.

- **Avoid superfluous information:** There is rarely a need to use the words “image”, “icon”, or “picture” in the alt text. 
- **Handle complex images as a special case:** Complex images such as graphs, charts, maps, and     illustrations contain substantial information – more than can be conveyed in a short phrase or sentence. In these cases, a two-part text alternative is required. The first part is the short description to identify the image and, where appropriate, indicate the location of the long description. The     second part is the long description – a textual representation of the essential information conveyed by the image. 

If you want to learn more about creating good alt text, I recommend the W3 alt decision tree site as a resource: https://www.w3.org/WAI/tutorials/images/decision-tree/ This site guides you with simple "yes/no" questions on how to create your alt text.

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/117.jpg' alt='117' width='500px' />

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/118.jpg' alt='118' width='500px' />

**Insert icon through [Font Awesome](https://fontawesome.com/icons):**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>My First Page</title>
    <link rel='stylesheet'
    href='https://use.fontawesome.com/releases/v5.8.1/css/all.css'
    integrity='sha384-50oBUHEmvpQ+1lW4y57PTFmhCaXp0ML5d60M1M7uH2+nqUivzIebhndOJK28anvf'
    crossorigin='anonymous'
  </head>
  <body>
    <i class="fab fa-500px"></i>
  </body>
</html>
```

**Ajust the size of the icon:**

```html
    <i class="fab fa-500px"></i>
    <i class="fab fa-500px fa-xs"></i>
    <i class="fab fa-500px fa-md"></i>
    <i class="fab fa-500px fa-lg"></i>
    <i class="fab fa-500px fa-2x"></i>
    <i class="fab fa-500px fa-3x"></i>
    <i class="fab fa-500px fa=5x"></i>
    <i class="fab fa-500px fa-10x"></i>
```

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/119.png' alt='119' width='400px'/>

**Use the icon for hyperlink:**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>My First Page</title>
    <link rel='stylesheet'
    href='https://use.fontawesome.com/releases/v5.8.1/css/all.css'
    integrity='sha384-50oBUHEmvpQ+1lW4y57PTFmhCaXp0ML5d60M1M7uH2+nqUivzIebhndOJK28anvf'
    crossorigin='anonymous'
  </head>
  <body>
    <i class="fab fa-500px"></i>
    <br />
    <a href="http://www.linkedin.com"><i class="fab fa-linkedin fa-5x"></i></a>
    <br />
  </body>
</html>
```

<img src='https://github.com/siyinghan/Notes/raw/master/Web%20Design%20for%20Everybody%20(Coursera%20Specialization)/01%20Introduction%20to%20HTML5/Image/120.png' alt='120' width='150px'/>

By adding in these aria labels, you're basically giving screen readers the ability to tell somebody where this link is going to go, to read a label. This is a huge in terms of accessibility:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>My First Page</title>
    <link rel='stylesheet'
    href='https://use.fontawesome.com/releases/v5.8.1/css/all.css'
    integrity='sha384-50oBUHEmvpQ+1lW4y57PTFmhCaXp0ML5d60M1M7uH2+nqUivzIebhndOJK28anvf'
    crossorigin='anonymous'
  </head>
  <body>
    <i class="fab fa-500px"></i>
    <br />
    <a href="http://www.linkedin.com" aria-label="LinkedIn"><i class="fab fa-linkedin fa-5x"></i></a>
    <br />
  </body>
</html>
```

