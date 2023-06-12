Welsim.com
========

Official website for the [WelSim](https://www.welsim.com/) - #1 engineering simulation software for the open source community.

Development
-----------

To set up your environment and run the server locally:

```bash
gem install bundler
git clone --depth 1 https://github.com/WelSimLLC/welsim.github.io.git
cd welsim.github.io
bundle install
bundle exec jekyll serve
```

More detailed instructions available at the [GitHub Pages documentation](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/). Really, GitHub? Yep. Really.

### Videos

To ensure videos work in Chrome/Firefox/Safari/Edge, videos should be encoded as H.264 MP4. For example:

```bash
# use this command to generate the H.264 MP4 version of the video
ffmpeg -i assets/WelSim_Launch_original.mp4 -vcodec h264 -acodec aac -strict -2 -movflags +faststart assets/WelSim_Launch.mp4 # convert video (in any supported format) into H.264 MP4
```

Then, generate a thumbnail for the video, used as a fallback (when the browser doesn't support video) or shown before the video is loaded:

```bash
# extract frame at 0 hours, 0 minutes, and 15 seconds into the video, save it as a JPG
ffmpeg -ss 00:00:15 -i assets/WelSim_Launch.mp4 -vframes 1 -q:v 2 assets/WelSim_Launch.jpg
```

Now that you have the H.264 MP4, and the thumbnail JPG, use the following markup in your HTML to include the video (with our cross-browser video component):

```
{% include video.html id="some-unique-identifier-for-video" path="/assets/WelSim_Launch.mp4" mimetype="video/mp4" thumbnail="/assets/WelSim_Launch.jpg" %}
```

Deployment
----------

Push to a GitHub repository, making sure the repository is set up with `https://www.welsim.com` as a [custom domain name](https://help.github.com/articles/using-a-custom-domain-with-github-pages/).

Content Management
------------------

### SEO

On any page, front matter entries can be used to add social media metadata. For example, on a blog post:

```markdown
# post-specific fields (other fields also may be used in the post, but also are used for SEO)
layout: post
date:   2019-04-04

# also used as title of card preview on Twitter and Facebook
title:  "Yeoh hyperelastic model for nonlinear finite element analysis"

# thumbnail image (note: must be a full URL, so it has to start with `https://welsim.com/...`)
# note: this defaults to https://welsim.com/android-chrome-384x384.png
# note: test this using https://cards-dev.twitter.com/validator and https://developers.facebook.com/tools/debug/sharing/
image: https://welsim.com/android-chrome-384x384.png

# description of the current page
# note: this defaults to the first paragraph of the content
description: "This is a blog post on WelSim's blog."

# content language
lang: en
```

### Frequently Asked Questions

To add a new FAQ entry, create a new file at `collections/_faq/<ORDER_WITHIN_PAGE>-<IDENTIFIER>.<LANGUAGE_CODE>.md` with the following form:

```markdown
---
lang: en # this post is written in English
order: 2 # this FAQ entry appears as the second entry
title: "QUESTION?"
---

ANSWER TO QUESTION.
```

Make sure to create the corresponding translated files for every language code!

To edit an existing FAQ entry, edit the corresponding file at `collections/_faq/<ORDER_WITHIN_PAGE>-<IDENTIFIER>.md`.

### News Articles

To add a new News Article, create a new file at `collections/_news/<YYYY>-<MM>-<DD>-<IDENTIFIER>.md` with the following form:

```markdown
---
title: "These are the Top Civil Engineering Startups in Pennsylvania (2021)" # title of the news article
weblink: "https://startupill.com/these-are-the-top-civil-engineering-startups-in-pennsylvania-2021/"   # link to online publisher's article
date: 2017-11-08                                                            # publication date of news article
thumbnail: "/assets/techcrunch.png"                                         # thumbnail shown with the article
source: startupill                                                          # publisher name
jumbotron: false                                                            # when `true`, shows the article in jumbotron at the top of the page, otherwise shows the article in articles list below
---

THIS MARKDOWN CONTENT IS SHOWN IN THE JUMBOTRON BOX, BESIDE THE THUMBNAIL, IF THE `jumbotron` SETTING IS `true` IN THE METADATA ABOVE. OTHERWISE, IT IS IGNORED.
```

### News Article Thumbnail

Desktop and mobile news article thumbnails have different proportions. In order for the thumbnail to appear properly in both contexts, do the following:

Create a 1000 x 750 px image file with 100 px margins, place news source logo inside the 800 x 550 px area and save as jpg or png.

To edit an existing News Article entry, edit the corresponding file at `collections/_news/<YYYY>-<MM>-<DD>-<IDENTIFIER>.md`.

### Blog Posts

To add a new Blog Post, create a new file at `collections/_posts/<YYYY>-<MM>-<DD>-<IDENTIFIER>.<LANGUAGE_CODE>.md` with the following form:

```markdown
---
lang: fr                                                                          # this post is written in French
layout: post                                                                      # use standard blog post page layout
title: "A Free Material Editing Tool - MatEditor" # title of the blog post
date: 2018-06-18                                                                  # publication date of blog post
author: "[Some Person](https://google.com)"                                       # author name (supports Markdown for links and formatting)
---

CONTENT OF BLOG POST AS MARKDOWN.
```

Make sure to create the corresponding translated files for every language code!

To edit an existing Blog Post entry, edit the corresponding file at `collections/_posts/<YYYY>-<MM>-<DD>-<IDENTIFIER>.<LANGUAGE_CODE>.md`.

#### Set When a Post Gets Published - Date and Time
You can set the date and time for when a blog post gets published. Instead of only a `YYYY-MM-DD` date in the blog post front matter you can include a time as well. The date and time is in [ISO 8601 format](https://www.w3.org/TR/NOTE-datetime). There is more than one way to write a date and time in ISO 8601 format, but to keep things simple, use this format: `YYYY-MM-DDTHH:MM±HH:MM`

Going left to right:
* `YYYY-MM-DD` is the standard year-month-day format.
* `T` is the letter "T" to indicate the following numbers are time.
* `HH:MM` is the time in the time zone you want the post to get published in. `HH` is 00 to 23. There is no AM or PM.
* `±HH:MM` this is the time offset from UTC for the time zone youw ant the post to get published in. `HH` is 00 to 23. There is no AM or PM.

Example: If you want a post to get published on March 15, 2022 at 9 AM PST you would have this in the front matter: 
```yaml
date: 2022-03-15T09:00-08:00
```

Since PST is 8 hours behind UTC, we use `-08:00` as the UTC offset after the `09:00`.


### Investors

To add a new Investor entry, create a new file at `collections/_investor_pics/<ORDER_WITHIN_PAGE>-<IDENTIFIER>.md` with the following form:

```markdown
---
pic_url: "/assets/a16z.png"  # thumbnail image for investor entry
name: "Andressen Horowitz"   # name of investor
web_url: "https://a16z.com/" # investor's website
order: 2                     # this is the second entry in the investors list
---
```

To edit an existing Investor entry, edit the corresponding file at `collections/_investor_pics/<ORDER_WITHIN_PAGE>-<IDENTIFIER>.md`.

Acknowledgement
--------------------
[chia-network.github.io](https://github.com/Chia-Network/chia-network.github.io).
