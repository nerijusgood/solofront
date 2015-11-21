---
title: 'Customize Twitter Widget css (style) for any website'
published: true
date: '21-12-2014 17:34'
summary:
    enabled: '1'
    format: short
taxonomy:
    tag:
        - js
        - tricks
    category:
        - blog
---

I recently encountered a situation where I needed to show twitter widget feed, more precisely a specific hashtag feed, in very custom styling: three columns in one row and, of course, make it responsive for different layout on smaller devices. In this post I will show how to customize twitter widget css, style and layout to fit your website.</p>

##1. Get Twitter widget ID
Let's cut the chase, go create widget like you would normally in your twitter account and choose what kind of content you want to pull - your feed, someone else's feed or a custom query search (like a #hashtag). After saving it, you can find the ID of the widget in the URL (string of numbers), like shown in example:

![Customize twitter widget css ID string](https://www.nerijusgood.com/wp-content/uploads/2014/12/twitter-widget-id.jpg)

##2. Fetch Twitter feed with small JS
I spent some time testing few methods of how to pull twitter feed into your website, the easiest and most customizable way was the " <a rel="nofollow" href="https://github.com/jasonmayes/Twitter-Post-Fetcher" title="Twitter Post Fetcher">Twitter-Post-Fetcher</a>" git project by jasonmayes. It works fine with new Twitter 1.1 API, which is necessary to pull feeds.

Now you just need to load this minified js file to your html and add twitter widget ID(s) to js and appropriate html tag IDs to show where to output the information. The Twitter Fetchers has more features and settings, but you can use the one I have pre-made to save you some time.

```javascript
var config1 = {
  "id": '539781433225932800',
  "domId": 'tw-widget1',
  "maxTweets": 1,
  "enableLinks": true
};
twitterFetcher.fetch(config1);
```

##3. Customize the widget
Here is the fun part - customize twitter widget css. The js will spawn the desired feed in very simple html markup, which is easy to target and manipulate via css (or sass, like in my example). Even though, the markup is in very specific order, which could probably be better it is still possible to change their position with css trickery. Here is the html output example:

```markup
<ul>
    <li>
        <div class="user">
            <a href="https://twitter.com/nerijusgood" aria-label="Nerijus (screen name: nerijusgood)" data-scribe="element:user_link">
                <img alt="" src="https://...img.png" data-src-2x="https://...2ximg.png" data-scribe="element:avatar">
                <span>
                    <span data-scribe="element:name">Nerijus</span>
                </span>
                <span data-scribe="element:screen_name">@nerijusgood</span>
            </a>
        </div>
        <p class="tweet">
        tweet content, which may have links and hashtags
        </p>
        <p class="timePosted">Posted on 19 Dec</p>
        <p class="interact">
            <a href="https://..." class="twitter_reply_icon">Reply</a>
            <a href="https://..." class="twitter_retweet_icon">Retweet</a>
            <a href="https://..." class="twitter_fav_icon">Favorite</a>
        </p>
    </li>

    <li>
    	another feed tweet
    </li>
</ul>
```

If you look closely, almost all elements have classes or specific data attribute (<em>data-scribe="something"</em>)  that you can target. The rest is up to your creativity, feel free to get inspired with my examples.

Please share your examples in the comments.