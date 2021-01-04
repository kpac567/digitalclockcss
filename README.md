1. Overview

  Pure Digital CSS clock. No JavaScript, no HTML(*). Not even for the
  text.

  Looks something like this, but something happens every second!

    |  --\    /-\  /-\    /-\  /-\
    |    |    | |  | |    | |  | |
    |  /-/    | |  | |    | |  | |
    |  |      | |  | |    | |  | |
    |  \--    \-/  \-/    \-/  \-/


Q: Why build a digital clock?
A: An analog pure css clock is banal at best.


Q: Why the asterisk after HTML.
A: (*) Browser's implicit HTML elements are used. I also have to explicitly set
   the <link> tag because most browsers don't support Link headers and
   stylesheets. See:
   https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Link
   https://bugs.chromium.org/p/chromium/issues/detail?id=692359


Q: Clock always starts at 12:00:00. Is this project a secret tribute to
   microwaves?
A: Perhaps.

Q: Ok, how does this work?
A: This kind of LCD display is called a 7-segment display. Each digit is split
   in seven segments. Depending on which segments are dark or light, the result
   looks like a digit between 0 and 9.

   In this hack, I used CSS animations to animate borders in a very specific
   way, resulting in the appearance of a digital clock. I need two HTML elements
   per digit.


Q: How do you avoid using any HTML?
A: Browsers automatically create implicit HTML nodes when a document is bare. In
   my case, I set the <link> tag and get implicit <html>, <head>, and <body>
   tags. This might not seem enough but I can use ::before and ::after
   selectors, resulting in exactly the 12 nodes I need.


Q: Why do you set content: ""?
A: Without setting content, ::before and ::after nodes are invisible.


Q: Why do you set display: block?
A: Without setting the display attribute, html, head, and link are invisible.


Q: Why do you set border: 1px solid #fff?
A: Safari doesn't animate attributes which haven't previously been set.


Q: What's the clip-path?
A: CSS borders provide a natural bevel which lines up with how 7-segment
   displays are supposed to look. I used the clip-path to get a similar bevel
   effect on the outer corners.


Q: Why do you set box-sizing: border-box?
A: It solves a pixel rounding issue with Safari. I use vw, vh, and vmin to make
   the clock look good and centered irrespective of the screen size. This can
   cause rounding issues since a box might land on the boundary of two pixels.
   CSS doesn't offer a ton of control when it comes to pixel rounding, but
   box-sizing seems to work ¯\_(ツ)_/¯.
