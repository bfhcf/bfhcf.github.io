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

### Adding New Events / Announcements
1. Go to `_events` directory
2. Create a new markdown file with the format `yyyy-mm-dd-title.md`
    * The date in the file is the date of posting or in other words, when you want this event post displayed. If you want this display now, use today's date.
3. Example of the contents of the markdown file should be as follows (please read on [markdown syntax](https://www.markdownguide.org/basic-syntax/)):
```
---
title: Practical Money Management 
speaker: Francis Kong
ministry: mkb
event_date: 2019-09-27 (Optional, if not set, post will be displayed always)
image: 2019-09-27-mkb-practical-money-management.jpg 
---

Content writeup about the post is written here. 
```

#### Fields
 * title - the title of the event
 * speaker - name of speaker (Optional and can be removed)
 * ministry - See `ministries.yml` for `slug` for each ministry
 * event_date - The date of the event in yyyy-mm-dd format (Optional, if not set, post will be displayed always)
 * image - The file name of the image that is uploaded to Cloudinary. Need Cloudinary Access to upload photos

**Note:** Layout is automatically set to 'event' through collection defaults in `_config.yml`

### Cloudinary Image Management
Images are stored on Cloudinary. The configuration is in `_config.yml` under the `cloudinary` section.

To use the Cloudinary URL helper:
```liquid
{% include cloudinary-url.liquid path='events/event-image.jpg' transforms='c_scale,w_594' %}
{{ cloudinary_url }}
```

Legacy URLs (e.g., `site.events_images_url`) are still supported but the new Cloudinary helper is recommended for new code.

### Color System

The website uses a centralized color system for consistent branding.

#### Available Colors
- **red**: #ff5139
- **green**: #58c31e
- **teal**: #3b8686
- **purple**: #906090
- **yellow**: #ffdf3e
- **orange**: #fea51b
- **cyan**: #00cbcb
- **lime**: #a1de45
- **black**: #000000

#### Usage in HTML
```html
<h1 class="color-bfhcf-teal">Title</h1>
<div class="bg-bfhcf-purple">Content</div>
```

#### Color Definitions
- **Data File**: `_data/colors.yml` (for Liquid templates)
- **SCSS Variables**: `assets/css/custom/_variables.scss`
- **CSS Classes**: `assets/css/custom/_colors.scss`

When modifying colors, update all three locations to maintain consistency.

### Reusable Components

The codebase includes reusable components in `_includes/`:
- `ministry-info.liquid` - Ministry logo and color logic
- `event-card.liquid` - Event card display
- `page-header.liquid` - Page headers with hero images
- `nav-active.liquid` - Navigation active state
- `cloudinary-url.liquid` - Cloudinary URL generation
- `utils/format-date.liquid` - Date formatting helper
- `utils/btn-circle.liquid` - Circular button component
- `utils/member-image.liquid` - Member image URL generator
