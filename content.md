# Search Engine Optimization (SEO) 🚀

## Introduction

Welcome to the dynamic world of SEO, where visibility is key, and the right
tweaks can put you ahead of the competition. This lesson will guide you through
essential steps and tools to enhance your website's search ranking, making it
easier for your audience to discover you online.

## Getting Started with Google Search Console

[Google Search Console (GSC)](https://search.google.com/search-console) is your
go-to tool for monitoring how Google views your site. It helps you understand
your site’s performance in search results and optimizes your ranking.

### Steps to Set Up GSC

- **Sign Up**: First, access Google Search Console
  [here](https://search.google.com/search-console/welcome).
- **Add Your Website**: Click on 'Add Property' to start adding your website.
- **Verify Ownership**: Google needs to confirm that you're the rightful owner
  of the website. This can be done through several methods, such as uploading a
  file to your server or adding a meta tag to your homepage.
- **Submit Your Sitemap**: Post-verification, submit your sitemap in XML format.
  This helps Google better understand the structure of your site.
  [Sitemap Generator](https://github.com/kjvarga/sitemap_generator) Gem can
  automate this for you.

## Enhancing Your SEO with Powerful Tools

### Webmaster Tools

Use [Ahrefs Webmaster Tools](https://ahrefs.com/webmaster-tools) to get a
comprehensive look at your website’s health, performance, and areas for
improvement.

### Keyword Analysis

- **Keyword Rank Checker**: Check how well your site ranks for your target
  keywords using
  [Ahrefs' Keyword Rank Checker](https://ahrefs.com/keyword-rank-checker).
- **Keyword Difficulty**: Find out how hard it would be to rank for specific
  keywords using
  [Ahrefs' Keyword Difficulty Tool](https://ahrefs.com/keyword-difficulty).

### Page Speed

Speed is a critical factor in SEO. Use
[Google's PageSpeed Insights](https://pagespeed.web.dev/) to analyze and
optimize the load times of your pages.

### Meta Tags

Meta tags are snippets of text that describe a page’s content; they’re key for
search engines and affect how content is displayed to visitors. Use
[Metatags.io](https://metatags.io/) to edit and experiment with your content
then preview how your webpage will look on Google, Facebook, Twitter and more.

## Crafting a SEO Strategy

### Understanding Keywords

The backbone of SEO is effective keyword use. You want to identify less
competitive, high-volume keywords to target. This means finding a niche within
broad topics. For instance, rather than targeting "Chicago", you might focus on
"vintage bookstores in Chicago".

### Content Creation

Once you have your keywords:

- **Create Quality Content**: Write useful, comprehensive content that
  incorporates your keywords naturally.
- **Update Regularly**: Keep your site fresh with regular updates and new
  information.

## SEO Best Practices

- **Responsive Design**: Ensure your website is mobile-friendly.
- **Internal Linking**: Use internal links wisely to allow search engines to
  crawl more deeply into your site.
- **Alt Text for Images**: Describe your images using alt text to improve
  visibility in search engine image results.

## Coding Exercise: Add Meta Tags to Your Application

Meta tags are crucial for SEO as they provide search engines with metadata about
the content of your pages. This section will guide you through adding and
customizing meta tags in your application.

### Step 1: Install the Meta Tags Gem

First, add the meta-tags gem to your Gemfile to help with managing all meta tags
in your app:

```ruby
gem "meta-tags"
```

Run `bundle install` to install the gem.

### Step 2: Set Up Default Meta Tags

Create a partial at `app/views/shared/_meta_tags.html.erb`:

```erb
<!--app/views/shared/_meta_tags.html.erb-->
<meta name="viewport" content="width=device-width,initial-scale=1">
<%= csrf_meta_tags %>
<%= csp_meta_tag %>
<%=
  display_meta_tags({
    site: "My Awesome App",
    image: asset_url('my-image.jpeg'),
    description: "The best app for posting about stuff",
    og: {
      title: "My Awesome App",
      image: asset_url('my-image.jpeg'),
      description: "The best app for posting about stuff",
      site_name: "My Awesome App"
    },
  })
%>
```

Incorporate these default meta tags in your layout by updating
`app/views/layouts/application.html.erb`:

```erb
<!--app/views/layouts/application.html.erb-->
<!DOCTYPE html>
<html>
  <head>
    ...
    <%= render "shared/meta_tags" %>
    ...
  </head>
  <body>
    <%= yield %>
  </body>
</html>
```

### Step 3: Customize Meta Tags for Specific Pages

For pages needing custom meta tags, set them in the corresponding controller
action:

```ruby
class MyController < ApplicationController
  def show
    set_meta_tags @record.to_meta_tags
  end
end
```

Implement the `to_meta_tags` method for your model. This way you'll have access
to data specific to that record. You might consider keeping this logic in a
concern `MetaTaggable`.

```ruby
# app/models/concerns/post/meta_taggable.rb
module Post::MetaTaggable
  extend ActiveSupport::Concern

  def to_meta_tags
    {
      site: "Readit",
      title: title,
      image: image_path,
      description: body.truncate_words(20),
      og: {
        title: title,
        image: image_path,
        description: body.truncate_words(20),
        site_name: "Readit",
      }
    }
  end

  def image_path
    if author.avatar.attached?
      Rails.application.routes.url_helpers.rails_blob_path(author.avatar)
    else
      ActionController::Base.helpers.asset_url('default_avatar.png')
    end
  end
end
```

### Step 4: Testing Meta Tags

To see how your meta tags appear in search results you can use a tool like
[Metatags.io](https://metatags.io/). If your app is running locally and you want
to test how it looks online, use [ngrok](https://ngrok.com/).

1. Install ngrok on macOS: `brew install --cask ngrok`
2. Run `ngrok http [port number]` in your terminal (default is usually port
   3000). This provides a forwarding URL which you can then use on metatags.io
   for testing, or share with friends while developing.

```plaintext
Forwarding                    https://d46c-38-32-143-226.ngrok-free.app -> http://localhost:3000
```

3. Use the forwarding to test your metatags at
   [Metatags.io](https://metatags.io/)

By following these steps, you ensure that each page of your application has
relevant and optimized meta tags, enhancing your SEO and improving your
visibility in search engine results.

## Conclusion

SEO is an ongoing process that requires patience and persistence. By using the
right tools and strategies, you can significantly enhance your site's visibility
and user traffic. Remember, the goal is not just to attract visitors but to
provide valuable content that keeps them coming back. Happy optimizing! 🌟
