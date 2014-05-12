---
layout: page
title: FrontEnd Standards
---

## SASS/CSS best practices

Don't over qualify class or ID selectors. On new projects style elements with classes
and tags only. Leave IDs for javascript hooks. On previous projects to


#### !important
There is only one use case for !important. The use case is to style a plugin or element
not in your code base which has a inline style or a !important itself. If you have to use an !important
please add a comment after it stating what you are overridding.

{% highlight scss %}
.disqus h2 {
	color: #fff !important; // Overriding inline style on Disqus plugin
}
{% endhighlight %}


#### Z-index
Only use high z-indexs when needed. If you use one please leave a comment to let people
know the reason for it.

{% highlight scss %}
header {
	position: fixed;
	z-index: 99999999; // This sticky-nav needs to be above google ads which can have a very high z-index
}
{% endhighlight %}


#### Nesting in SASS
You should try and never nest your SASS more than three layers deep.

{% highlight scss %}
.header {
  .nav-bar {
    li {
      // no more!
    }
  }
}
{% endhighlight %}

## Javascript best practices

## Gulp.js


<a href="http://gulpjs.com/"><img src="https://raw2.github.com/gulpjs/artwork/master/gulp-2x.png" width="80" alt="Built with Gulp"></a>


#### Dependencies

Majors:

* Node.js
* Ruby

Secondaries:

* Node: npm
* Ruby: Sass 3.3.x

After you've set this stuff up please run

	$ npm install -g gulp

Open your .bash_profile or .bash_rc file and enter the following line

	ulimit -S -n 8192

This installs the Gulp command line tools
Afterwards please run

	$ npm install

in your project's directory.
This will install all the things you need for running the gulp-tasks
automatically.

Now Gulp should be installed and all you need to type is gulp to run it

	$ gulp



## SASS

We are currently working with [Sass](http://sass-lang.com/) (in its dialect
SCSS) and do not use CSS directly. Please do not edit the CSS-files in any case
but search the corresponding `.scss` file and edit it accordingly. If you are
not familiar with SCSS you can write pure CSS which is actually valid SCSS.

You can find more information about the installation process of Sass and the
usage of SCSS in the [Sass Tutorial](http://sass-lang.com/tutorial.html).
