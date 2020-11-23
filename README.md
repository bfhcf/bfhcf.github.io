## Welcome to Bread From Heaven Christian Fellowship Website
#### Powered by Jekyll / Github Pages

Setup for Developers
====================
1. Clone the Repository on your local machine
2. Install jekyll bundler by running `gem install jekyll bundler`
3. run `bundle install`
4. run `bundle exec jekyll serve`
5. Go to `localhost:4000` to view your site


Architecture
====================
Read [Jekyll Architecture](https://jekyllrb.com/docs/structure/) on how a Jekyll File Structure looks like.

Main site config is stored in `_config.yml`  
Other data are stored in `_data` directory in `.yml` format. 

###Adding New Events / Announcements
1. Go to `events/_posts`
2. Create a new markdown file with the format `yyyy-mm-dd-title.md`
    * The date in the file is the date of posting or in other words, when you want this event post displayed. If you want this display now, use today's date.
3. Example of the contents of the markdown file should be as follows (please read on [markdown syntax](https://www.markdownguide.org/basic-syntax/)):
```
---
layout: default
title: Practical Money Management 
speaker: Francis Kong
ministry: mkb
event_date: 2019-09-27 (Optional, if not set, post will be displayed always)
image: 2019-09-27-mkb-practical-money-management.jpg 
---

Content writeup about the post is written here. 
```

#####Fields
 * layout - should be set to default
 * title - the title of the event
 * speaker - name of speaker (Optional and can be removed)
 * ministry - See `ministries.yml` for `slug` for each ministry
 * event_date - The date of the event in yyyy-mm-dd format (Optional, if not set, post will be displayed always)
 * image - The file name of the image that is uploaded to Cloudinary. Need Cloudinary Access to upload photos