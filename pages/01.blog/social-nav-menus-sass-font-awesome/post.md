---
title: 'Smart social nav menus with SASS and Font Awesome'
published: true
publish_date: '09/11/2014 12:00 am'
taxonomy:
    tag:
        - CSS
summary:
    enabled: '1'
    format: short
---

This post is an addition to Justin Todlock's 'Social Nav Menus' tutorial series on how to include social sharing links to your WordPress (or any other) website. You can find the original posts here: <a href="http://justintadlock.com/archives/2013/08/07/social-media-nav-menus" title="Justin Todlocks social nav pt1" target="_blank">part one</a> and <a href="http://justintadlock.com/archives/2013/08/14/social-nav-menus-part-2" title="Justin Todlocks social nav" target="_blank">part two</a>. </p><p>Justin Todlock has provided us with an excellent way how to deal with social sharing link design in our websites by targeting link html attribute. I think this is a very smart way to solve this issue, however I am a big fan of SASS and I believe that his method can be simplified a little bit more. Before we dig into SASS I will go through the Justin's method so we would be on the same page (of course you can fallow the <a href="http://justintadlock.com/archives/2013/08/07/social-media-nav-menus" title="Justin Tadlock: social nav menus" target="_blank">original posts</a> too).

##Create a new social menu (WordPress)
Open your <em>functions.php </em>and copy/paste code bellow. This code will register a new menu in you WordPress theme.

```javascript
function register_my_menu() {
    register_nav_menu('social-menu',__( 'Social Menu' ));
}
add_action( 'init', 'register_my_menu' );
```

Now you can find the new menu in your dashboard menu, Menu Locations settings, but even if you put something in it you will not find it in your website - we need to tell theme where the menus will appear. However we need to modify original markup so we could design menu the way we want. In the original post Justin suggests creating a specific <em>php</em> file for social menu markup function (create like a template file) and then call it in your themes desired location. Well, its an option, but I rather keep all of my settings in one place. <br /><br />Customizing theme constantly requires having extra functions and settings changed, therefore I have an extra <em>php</em> only for that. It is like an addition to my <em>functions.php</em>, but it only includes functions that are secondary relevance to my theme: functions which are not essential for theme to work. This way I keep my <em>functions.php</em> and theme folder organized and clean.

```javascript
function redefined_reality_social_menu() {
	if ( has_nav_menu( 'social' ) ) {
		wp_nav_menu(
			array( 'theme_location'  => 'social',
				'container'       => 'div',
				'container_id'    => '',
				'container_class' => 'social-menu',
				'menu_id'         => '',
				'menu_class'      => 'social-menu-ul',
				'depth'           => 1,
				'link_before'     => '<span class="screen-reader-text">',
				'link_after'      => '</span>',
				'fallback_cb'     => '',
			)
		);
	}
}
```

Well its easy to understand how we customize markup here, right? Also, I bet you noticed how I added span around my link, this will be handy when styling.  Also, you can remove empty elements, I left them just to show possibilities.

##Add the menu to your desired place</h2>
Now its time to add the theme. It is completely up to you where you want to add your custom menu. You just need to take the code bellow and add it to your template files. Also, you can go to widget settings and add a custom menu to any of your sidebars or post templates.

```php
<?php name_social_menu(); ?>
```

Well styling the markup and locating your theme is entirely up to you. You can read more about custom navigation in <a href="http://codex.wordpress.org/Navigation_Menus" title="Nav menus" target="_blank">WP Codex</a>.

##Style the menu (Sass way!)
Now, its time to use magic of Todlocks method and Sass to make long list of social link styling a peace of cake. If your previous steps were correct your markup should spawn something like this:

```markup
<div class="social-menu">
	<ul id="menu-social-links-1" class="social-menu-ul">
		<li class="menu-item..."><a href="https://www.facebook..."><span class="screen-reader-text">Facebook</span></a></li>
		<li class="menu-item..."><a href="http://twitter..."><span class="screen-reader-text">Twitter</span></a></li>
		<li class="menu-item..."><a href="https://plus.google..."><span class="screen-reader-text">Google +</span></a></li>
		<li class="menu-item..."><a href="https://www.linkedin..."><span class="screen-reader-text">LinkedIn</span></a></li>
		<li class="menu-item..."><a href="http://stackexchange..."><span class="screen-reader-text">Stack Exchange</span></a></li>
		...
	</ul>
</div>
```

So, now using Todlocks method we target elements by their <i>href</i> attribute. However, the css would look messy since we would have to assign each social link icon and colour styling manually. It is fine if you want to use several social links, but if you want an universal solutions with option to easy add new social networks, than <i>Sass</i> is the way to go. We will use <i>Sass For</i> directive to loop through each social network in the list:

```sass
$network_names: twitter, facebook, google, linkedin, pintrest, tumblr, vk, xing, dribbble, github
$network_urls: "twitter.com", "facebook.com", "plus.google.com", "linkedin", "pinterest", "tumblr", "vk.com", "www.xing-share", "dribbble.com", "github.com"
$network_colors: #00aced, #3b5998, #dd4b39, #007bb6, #cb2027, #32506d, #5e82a8, #175e60, #ea4c89, #175e60, black
$network_icons: "\f099", "\f09a", "\f0d5", "\f0e1", "\f0d2", "\f173", "\f189", "\f168", "\f17d", "\f09b"

@for $i from 1 through length($network_names)
	a
		&[href*='#{nth($network_urls, $i)}']::before
			content: nth($network_icons, $i)
	a[href*='#{nth($network_urls, $i)}']
		background-color: nth($network_colors, $i)
		&:hover
			background-color: lighten(nth($network_colors, $i), 5%)
```

So this magic loop will allow as to add any social network just by adding an entry to network_names, network_urls, network_colors and network_icons variables. Ta-daaaa. 

Well for me its pretty easy. Here is an example: 

<p data-height="307" data-theme-id="8674" data-slug-hash="hqxae" data-default-tab="result" data-user="nerijusgood" class='codepen'>See the Pen <a href='http://codepen.io/nerijusgood/pen/hqxae/'>Smart Social Nav for WordPress with Sass</a> by Nerijus (<a href='http://codepen.io/nerijusgood'>@nerijusgood</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

<p>In the end, we have easy to edit dynamic sass and a clean markup. Other than that, design is completely up to you. Good luck designing and coding.</p>