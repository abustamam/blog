---
layout: post
title: "Implementing Theme with Octopress and Jekyll Asset Pipeline"
date: 2014-07-31 11:32:53 -0700
comments: true
categories: 
---

The purpose of this post is simple. 

Octopress does not have much documentation on installing themes. I know it is not the developer way to install a theme,
but it is the developer way to create themes. 

Here is what I've learned while trying to import a Start Bootstrap theme to Octopress. 

<!-- more -->

First, get to know the `rake install[optional theme name]` command. It's actually the first task in the Rakefile:


    desc "Initial setup for Octopress: copies the default theme into the path of Jekyll's generator. Rake install defaults to rake install[classic] to install a different theme run rake install[some_theme_name]"
    task :install, :theme do |t, args|
      if File.directory?(source_dir) || File.directory?("sass")
        abort("rake aborted!") if ask("A theme is already installed, proceeding will overwrite existing files. Are you sure?", ['y', 'n']) == 'n'
      end
      # copy theme into working Jekyll directories
      theme = args.theme || 'classic'
      puts "## Copying "+theme+" theme into ./#{source_dir} and ./sass"
      mkdir_p source_dir
      cp_r "#{themes_dir}/#{theme}/source/.", source_dir
      mkdir_p "sass"
      cp_r "#{themes_dir}/#{theme}/sass/.", "sass"
      mkdir_p "#{source_dir}/#{posts_dir}"
      mkdir_p public_dir
    end
 

What it does is scour the ./.themes directory and copies all the files from the `/source` and the `/sass` directories
into the root. 

Thus, a complete theme must contain `/source` and `/sass` directories. 

From there, if you run `rake generate` it will process the sourcefiles and build the site.