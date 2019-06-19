---
view: post
layout: post                          # Only in unique we use the "layout: post"
lang: en                              # Lang is required
author: op07n
title: Mono winforms on repl.it
description: 
excerpt: 
cover: false                          # Leave false if the post does not have cover image, if there is set to true
coverAlt: 
demo: 
categories:
  - vuejs
tags: 
  - vuejs
  - vuepress
  - static site
created_at: 2019-06-19 10:00
updated_at: 2019-06-19 10:00
meta:                                 # If you have cover image

---

[repl.it](https://repl.it/) is an online compiler used for compiling and running codes of various languages like Python , javascript etc.

At the moment there is no template for mono with winforms. To get that I used [polygott](https://github.com/replit/polygott)

[Polygott](https://github.com/replit/polygott) is a lot more flexible than other templates from **repl.it.**

I don't know how to initiate a new [polygott](https://github.com/replit/polygott) template, so I did a fork of an existing one.

I did a fork of [https://repl.it/@SPQR/Template-for-compilation-options](https://repl.it/@SPQR/Template-for-compilation-options).

And change the *Makefile* for this:

```bash
.PHONY: run

run:
	killall polygott-x11-vnc || true
	polygott-x11-vnc
	xrandr -s 800x600
	DISPLAY=:0
	csc hello.cs -r:System.Windows.Forms.dll
	chmod 744 /home/runner/hello.exe
	DISPLAY=:0.0 mono hello.exe
```

For test I used the file *hello.cs*:

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;
 
public class HelloWorld : Form
{
    static public void Main ()
    {
        Application.Run (new HelloWorld ());
    }
 
    public HelloWorld ()
    {
        Button b = new Button ();
        b.Text = "Click Me!";
        b.Click += new EventHandler (Button_Click);
        Controls.Add (b);
    }
 
    private void Button_Click (object sender, EventArgs e)
    {
        MessageBox.Show ("Button Clicked!");
    }
}
```

And here is embedded the result:

<iframe height="800px" width="100%" src="https://repl.it/@op07n/monowinforms?lite=true&outputonly=1" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>



