## Adding Disqus to a Jekyll blog

Having a blog based on static web pages doesn't give your visitors the possiblity to react on a blog post. This can be solved by using an external service like [Disqus][1]. For non-commercial websites you can subscribe to the plus plan for free. With the plus plan you don't have to show ads.

The [installation documentation][2] of using Disqus together with Jekyll is in my opinion a limited. The need of a *comment* variable is not needed when all your posts allow to have comments. 

I added the *Universal Embeded Code* to a *disqus.html* file within the *_includes* folder. While this code can be directly added to the *posts.html* layout file, I like to have this in two seperated files to keep things clear.

{% highlight html linenos %}
<div id="disqus_thread"></div>
<script>

var disqus_config = function () {
    this.page.url = '{{page.url | absolute_url}}';
    this.page.identifier = '{{page.url}}';
};

(function() {
    var d = document, s = d.createElement('script');
    s.src = 'https://johandekoning.disqus.com/embed.js';
    s.setAttribute('data-timestamp', +new Date());
    (d.head || d.body).appendChild(s);
})();
</script>

<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
{% endhighlight %}

On line 14 and 15 the page url and identifier are set. By using the liquid filer absolute url `{% raw %}{{page.url | absolute_url}}{% endraw %}` the page url will be prepend with the base url. For the identifier I didn't see the need of having an absolute url and therefore only the page.url is used.

Also make sure that you set the correct Disqus shortname on line 20. I my case *johandekoning*

Inside the *post.html* I include this disqus file on the position where the comments should be rendered: `{% raw %}{% include disqus.html %}{% endraw %}`

[1]: https://disqus.com/
[2]: https://johandekoning.disqus.com/admin/settings/jekyll/