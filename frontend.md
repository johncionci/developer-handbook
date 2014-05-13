---
layout: page
title: Frontend Standards
---

<a href="https://docs.google.com/a/thinkoomph.com/document/d/19PMZOq4KUQa9BYkbfmevRWf5DaDo52GDPQlczMa20_k/edit#">Guidelines</a>
<a href="https://docs.google.com/a/thinkoomph.com/document/d/1hgiQ7hrnfy7gWO9bv1twdcyyvBk2oSNekFxUZgunrGA/edit#">Tech Stack</a>

## Css

Don't over qualify class or ID selectors. On new projects style elements with classes
and tags only. Leave IDs for javascript hooks. On previous projects to

##### !important
There is only one use case for !important. The use case is to style a plugin or element
not in your code base which has a inline style or a !important itself. If you have to use an !important
please add a comment after it stating what you are overridding.

{% highlight scss %}
.disqus h2 {
	color: #fff !important; // Overriding inline style on Disqus plugin
}
{% endhighlight %}


##### Z-index
Only use high z-indexs when needed. If you use one please leave a comment to let people
know the reason for it.

{% highlight scss %}
header {
	position: fixed;
	z-index: 99999999; // This sticky-nav needs to be above google ads which can have a very high z-index
}
{% endhighlight %}

## Preprocessors

### Sass
We use Sass as our default CSS preprocessor (in its dialect SCSS). Sass is "the most mature, stable, and powerful
professional grade CSS extension language in the world." You should always have the latest version of Sass installed.
Visit [Sass](http://http://sass-lang.com/) to learn more.

**Never edit CSS files directly.** You should always edit the corresponding `.scss` file. If you are
not familiar with SCSS you can write pure CSS which is actually valid SCSS.

##### Nesting
You should try and never nest your SASS more than three layers deep. This will lead to long and ultra specific selectors
in your comiled CSS. As of Sass 3.3 you can use @at-root to break out of your nesting at anytime.

{% highlight scss %}
@media print {
  .page {
    width: 8in !important;
    @at-root (without: media) {
      width: 960px;
    }
  }
}
{% endhighlight %}

outputs

{% highlight css %}
@media print {
  .page {
    width: 8in !important;
  }
}
.page {
  width: 960px;
}
{% endhighlight %}

## Frameworks

We use Foundation as our default CSS frontend framework. Foundation is "The most advanced responsive
front-end framework in the world." It provides a fast simple way to protype and build our sites.
Visit [Foundation](http://http://foundation.zurb.com/) to learn more.

## Javascript

## Build Systems

### Gulp.js


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