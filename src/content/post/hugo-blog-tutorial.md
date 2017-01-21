+++
image = "hugo.png"
date = "2016-12-19T21:37:31-06:00"
title = "Hugo Blog Tutorial"
draft = false

+++

So I've started this new blog. Something a little easier to update than my [old blog](http://old.randomscribes.com). It's using a number of great technologies, Git (of course), Hugo, and Google's Appengine. This post is all about my experience with Hugo.

# Why Hugo?
Hugo is a static site generator. It's built on top of Go, pretty simple, and super fast. You write your content in markdown and after a quick save the built in server will automatically builds your static files on the fly. The site configuration can be written in JSON, YAML or TOML. The directory structure, which is used by Hugo to know which content to serve where, can get a little complicated, but as long as you stick to the documentation you'll be fine. You can use one of the existing [themes](http://themes.gohugo.io/), build your own... or if you are like me go without one (although I think they recommend always using themes).

# How'd I do it?
There is a [quick start guide](http://gohugo.io/overview/quickstart/) that I used from Hugo, my instructions diverge a little bit from it.

1. Install [Hugo](http://gohugo.io/) or 

    ``` 
    $ brew update && brew install hugo 
    ```

1. Create your new site 

    ```
    $ hugo new site random-scribes
    ```

1. You'll have a folder structure that looks something like this:

    ```
    .
    |-- archetypes
    |-- config.toml
    |-- content
    |-- data
    |-- layouts
    `-- static

    5 directories, 1 file
    ```

    Straight from the Hugo [quick start guide](http://gohugo.io/overview/quickstart/)
    * archetypes: You can create new content files in Hugo using the hugo new command. When you run that command, it adds few configuration properties to the post like date and title. Archetype allows you to define your own configuration properties that will be added to the post front matter whenever hugo new command is used.

    * config.toml: Every website should have a configuration file at the root. By default, the configuration file uses TOML format but you can also use YAML or JSON formats as well. TOML is minimal configuration file format that’s easy to read due to obvious semantics. The configuration settings mentioned in the config.toml are applied to the full site. These configuration settings include baseURL and title of the website.

    * content: This is where you will store content of the website. Inside content, you will create sub-directories for different sections. Let’s suppose your website has three actions – blog, article, and tutorial then you will have three different directories for each of them inside the content directory. The name of the section i.e. blog, article, or tutorial will be used by Hugo to apply a specific layout applicable to that section.

    * data: This directory is used to store configuration files that can be used by Hugo when generating your website. You can write these files in YAML, JSON, or TOML format.

    * layouts: The content inside this directory is used to specify how your content will be converted into the static website.

    * static: This directory is used to store all the static content that your website will need like images, CSS, JavaScript or other static content.



1. Now add some content... in my case I wanted to add a new post.

    ```
    $ hugo new post/hugo-blog-tutorial.md
    ```
    
    You'll see this file show up as `content/post/hugo-blog-tutorial.md`

1. Inside my brand new file, I find this lovely TOML configuration:

    ```
    +++
    date = "2016-12-19T21:37:31-06:00"
    draft = true
    title = "hugo blog tutorial"

    +++

    I added this as my first blog post's content.
    ```

    It's pretty straight forward, date the file was created, draft status (true/false), and title. Everything after the TOML configuration is the content for file written in markdown.

1. You can go download a [theme](https://themes.gohugo.io/) and throw it into a directory called `themes`. I tried that and got confused, going without a theme seemed more straight forward to me. However, if you are unsure of what you want your site to look like, and you were hoping to try a couple different themes, by all means install one and start the hugo server with the specified theme.

    ```
    $ hugo server --theme=hugo_theme_robust --buildDrafts
    ```

1. If you're still with me and decided against the theme thanks! Setting up your site is pretty straight forward, everything goes in you `layouts` directory.

    * First you'll probably want to set up your `partials` folder. I added a `header.html` and `footer.html`. You can guess the kind of content that would be included there.

    * Second, in your `layouts` create an `index.html`, this can contain whatever you want, but you'll probably want to include both your partials.

        ```
        {{ partial "header.html" . }}
        <main>
            <!-- some sort of content here -->
        </main>
        {{ partial "footer.html" . }}
        ```
    
    * Now you'll want to set up your `_default` folder.
        
        * Let's start with `section.html` do something simple like:

            ```
                {{ partial "header.html" . }}
                <main>
                    <div>
                        {{ range .Data.Pages }}
                            {{ .Render "li"}}
                        {{ end }}
                    </div>
                </main>
                {{ partial "footer.html" . }}
            ```

        * This will generate a page with a whole bunch of _li_. Those _li_ are your posts (or any other content that you've added to you `content` folder). In `_default` you'll want to add a `li.html` file.

            ```
            <div>
                <div>
                    <h2><a href="{{ .Permalink }}">{{ .Title }}</a></h2>
                    <div>
                        <span>{{ .Date.Format "Mon, Jan 2, 2006" }} {{ if .GetParam "draft"}}DRAFT{{end}}</span>
                    </div>
                    <div>
                        <p>{{ .Summary }} <a href="{{ .Permalink }}">Read full post &#10132;</a></p>
                    </div>
                </div>
            </div>
            ```

            Title's is the `.Title` and `.Date` are from the post markdown files. The `.Permalink` is the link to the post and some what obviously we are checking to see if this post is a draft so we can spit that out as a visual indicator. The `.Summary` is "A generated summary of the content for easily showing a snippet in a summary view. Note that the breakpoint can be set manually by inserting <!--more--> at the appropriate place in the content page". I love being able to control the breakpoint!
        * Finally you have `single.html`. This is how your post is going to be setup. For simplicity let's just have:

            ```
            {{ partial "header.html" . }}
            <section>
                <h1 id="title">{{ .Title }}</h1>
                <aside id="meta">
                    <h4 id="date"> {{ .Date.Format "Mon Jan 2, 2006" }} </h4>
                    <section>
                        <h5 id="wc"> 
                            {{ if gt (div .WordCount 250.0) 1 }}
                                {{ int (div .WordCount 250.0) }} Minutes
                            {{else}}
                                1 Minute
                            {{ end }}
                            of reading time
                        </h5>
                    </section>
                </aside>
                <div class="padding-8">
                    <article id="content">
                    {{ .Content }}
                    </article>
                </div>
            </section>
            {{ partial "footer.html" . }}            
            ```

            Most of this you've seen before except for a couple new variables. `.WordCount` as you may have guessed, is the number of words in your post. Likewise `.Content` is the content of the actually post. 

1. Now you are ready to start the Hugo server, with the `--buildDraft` option (or else you won't have any content).

    `$ hugo server --buildDrafts`

    You'll get some lovely output telling you what was create, the server address (http://localhost:1313/) and that Hugo is watching for any changes.

1. Check it out in your browser. Make some changes and see how fast Hugo rebuilds your site. When you're ready (and update some of your posts so that they are no longer in draft) just run `$ hugo` and Hugo will throw your built website in the `public` folder.


# Done
Well the Hugo part is done. You can checkout [GitHub](https://github.com/randomscribes/random-scribes) to see how I've evolved the blog over time. I've still got to setup up my Appengine instance and deploy the code and switch my old blog to a subdomain of my new one. That'll come in another post.