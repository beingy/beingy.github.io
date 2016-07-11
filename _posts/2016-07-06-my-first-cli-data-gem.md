---
layout: post
title: My First CLI Data Gem
navi_title: Blog Post
date: 2016-07-06 12:00:00 -0500
excerpt_separator: <!--more-->
---

So it finally happened.  I've created and published my first CLI data gem on [RubyGems.org](https://rubygems.org/gems/npr_best_books).  Here's how I did it and the [Github repo](https://github.com/beingy/npr-best-books-cli-gem) for reference.<!--more-->

I've also created my first walk-through video to demo how my CLI data gem works. Please see below.  Enjoy.

{% include youtube_embed.html id="tHA7F2oXPg4" %}

# How to build a CLI Data Gem

I had no idea where or how to get started so I got help and wrote down the list of to-do's to keep me focused and discover my way to determine the next steps in building a CLI data gem as I go from one milestone to another.

1. a) [Plan](#plan) your gem, b) [imagine](#imagine) your interface
2. Start with [project structure](#structure) - google `how to build a gem`, etc.
3. Start with the entry point - the codes to run the [CLI](#cli)
4. [Force](#force) that to build the CLI interface
5. [Stub](#stub) out the interface - fake it until you are ready to make it
6. Start [making things real](#make)
7. [Discover](#discover) objects
8. [Program](#program)

# <a name ="plan">Planning</a>

## Scope & Inspiration

The point of the CLI data gem basically want us to explore extracting data from an external source and interact with it in real time from a command line interface (aka CLI) in a text-only bash user interface.  The scope also wanted us to drill at least one level down to pull additional details from the initial data we gathered.

Sounds fun!  What's next?  Where do I want to "scrape" information from and display it in a useful manner and then provide additional information upon request?

*Being's mind at work*

I don't read as much as I think about reading.  Ever since I've started learning to code, I want to think less and do more so I have been reading a lot of science fiction books one after another on my hour long commute to and from Flatiron School campus in the Financial District.  And, for the longest time I always been looking for interesting books to read.  

Staying on my streak of reading daily on my commute, I started to track the books I read on [GoodReads.com](https://www.goodreads.com/user/show/53599856-being) so naturally I thought GoodReads was a great place to start.  I started checking out GoodReads' overwhelming lists of book recommendations and quickly shied away from attempting on the monumental task. *It was much later on while working on the CLI data gem that I realized I could have still scraped GoodReads with the right focus. I still might do it as a challenge as long I have narrowed down to a specific list.*

My next target was [NPR's Book Concierge](http://apps.npr.org/best-books-2015/) website that featured recent year's book reviews in various genres and provides a single list of book recommendations from book critics, journalists or notable curators year to year.  Bingo!

## <a name ="imagine">Imagine a CLI interface</a>
Now that I have an external source of data in mind, time to imagine my CLI interface and build it. I imagine the following:

1. Welcome loading screen to NPR's Book Concierge.
2. Lookup NPR's website and retrieve a list of book recommendations from the most recent year.
3. Ask user to enter a book number to learn more about the book one level down.
4. Display book details and ask user what they'd like to do next: list the books again or enter another book number or exit program.
5. Exit screen.

Short and simple. I think I'm almost ready to build the CLI user interface.  

Before I get ahead of myself. Before I start building, let's understand what individual objects we are working with.  By objects, I am referring to how do we define the data we are scraping from the external source. For the NPR's book recommendations, it seems to be pretty straight forward.  I am working with **a list of books** and going one level down, each **book has a list of attributes**.

Defining my objects:

### What is a list of books?

+ A list has_many books
+ A list has a year
+ A list has a genre/title

### What is a book?

#### Phase 1 (NPR)
+ A book belongs to a list (for now, may belong_to_many lists/genres later)
+ A book has a title
+ A book has an author
+ A book has a recommender
+ A book has a book review description
+ A book has a genre name per list
+ A book has an ISBN/ISBN13

#### Phrase 2 (Amazon)

+ A book has a publisher
+ A book has a number of pages
+ A book has a type (Hardcover or Paperback)
+ A book has an Amazon rating
+ A book has an Amazon price

Amazon was always the holy grail of ratings so I have been wanting to scrape Amazon's average ratings ever since I learned about scraping.

# Development

## <a name="structure">Getting started</a>

Now that I have a clear understanding of what I would like to do.  How do I begin to code?  Easy when we have a check list to go off of.  We begin by setting the gem.

## Setup Gem via Bundler

By far the easiest way for a beginner to setup a gem template with initial folders and files is by using `bundler`, by issuing the following command in bash:

If you haven't installed `bundler`, try this:

  {% highlight bash %}
  $ gem install bundler
  {% endhighlight %}

To setup my gem named `npr_best_books` using `bundler`, I did the following:

  {% highlight bash %}
  $ bundle gem npr_best_books
  {% endhighlight %}

This created a basic tree of directories and files that I need to create a gem.

Here are the resources that helped me to get started using Bundler:

+ [Step by Step to Guide to Building Your First Ruby Gem by Matt Huggins ](https://quickleft.com/blog/engineering-lunch-series-step-by-step-guide-to-building-your-first-ruby-gem/)
+ [RubyGems.org: Make your own gem](http://guides.rubygems.org/make-your-own-gem/)
+ [It's raining gems! How to build your own gems by PJ Hagerty](https://blog.engineyard.com/2015/its-raining-gems)

By the end of my CLI data gem, this is my tree:

  {% highlight bash %}
  $ tree
  .
  ├── CODE_OF_CONDUCT.md
  ├── Gemfile
  ├── Gemfile.lock
  ├── LICENSE.txt
  ├── NOTES.md
  ├── README.md
  ├── Rakefile
  ├── bin
  │   ├── console
  │   ├── npr_best_books
  │   └── setup
  ├── lib
  │   ├── npr_best_books
  │   │   ├── book.rb
  │   │   ├── cli.rb
  │   │   ├── list.rb
  │   │   ├── scraper.rb
  │   │   └── version.rb
  │   └── npr_best_books.rb
  ├── npr_best_books.gemspec
  ├── pkg
  │   ├── npr_best_books-0.2.0.gem
  │   └── npr_best_books-0.2.1.gem
  └── spec
      ├── npr_best_books_spec.rb
      └── spec_helper.rb

  5 directories, 31 files
  {% endhighlight %}

## GitHub Version Control

I am getting more comfortable using Git version control. I made sure to create a repo for my gem as soon as it was setup.  It was after I was done with the coding the gem that I found that Git version control was required to publish to Rubygem.org so make sure you commit and push to your repo often.

## <a name="cli">CLI</a> interface

At this point, I am finally ready to code the CLI.

I know I just need to make a functional CLI first and stub all the data feed from fake strings to have a working CLI.  Going from what I imagined my CLI would look like, I quickly created what would become my final CLI displays below.

I want to simply issue a command called 'npr_best_books' to start the gem and <a name="stub">stub</a> with fake string information to create a working prototype:

  {% highlight bash %}
  $ npr_best_books
  == Welcome to NPR's Book Concierge ==
  == A Guide to 2015's Great Reads ==
  Loading latest list...
  Loading books...
  2015's Science Fiction & Fantasy recommendations:
  1. The Sandman: Overture by Neil Gaiman, illustrated by JH Williams III
  2. Interstellar Cinderella by Deborah Underwood, illustrated and co-authored by Meg Hunt
  ...
  57. Tales From The Loop by Simon Stalenhag
  Total 2015 NPR Science Fiction & Fantasy recommendations: 57 books
  Enter the 'number' of the book you'd like to learn more about, or:
  'exit' to end program, 'more' to see recommendations from other years
  ==> Command:
  {% endhighlight %}

  And, if we enter command '1', additional info is displayed for Book 1:

  {% highlight bash %}
  ==> Command: 1
  ================================================================================
  => List ID: 1
  => Title: The Sandman: Overture
  => Author: Neil Gaiman, illustrated by JH Williams III
  => Recommended by: Sam Briger
  => Book Review:
     Best-selling author Neil Gaiman made his name writing the horror/fantasy
     comic book series _The Sandman_ about the godlike character Morpheus, the
     Lord of Dreaming. Its 75-issue run revealed Gaiman's seemingly limitless
     imagination — he wrote stories about a convention for serial killers, the
     gods that view hell as prime real estate for development once Lucifer
     abandons it, and the premiere of Shakespeare's _A Midsummer Night's Dream_
     held for an audience from the fairy realm. For the 25th anniversary of the
     comic book, Gaiman returned to his beloved characters for a six-issue
     miniseries. Here, Morpheus is tasked with saving the universe from complete
     destruction — a destruction he himself set in motion. _The Sandman: Overture_
     serves as a prequel to the original series and gives you the chance to read
     it all over again.
  => ISBN: 1401248969, ISBN-13 9781401248963
  => Average Amazon Customer Reviews:
     4.6 out of 5 stars (139 Reviews)
  ================================================================================
  What would you like to do next? Here are your options:
  Enter a book 'number' from the list to learn more, 'list' to show book list again,
  'exit' to end program.
  ==> Command:
  {% endhighlight %}

  Type 'list' to display the list of books again or enter another book 'number' for more info:

  {% highlight bash %}
  ==> Command: list
  2015's Science Fiction & Fantasy recommendations:
  1. The Sandman: Overture by Neil Gaiman, illustrated by JH Williams III
  2. Interstellar Cinderella by Deborah Underwood, illustrated and co-authored by Meg Hunt
  ...
  57. Tales From The Loop by Simon Stalenhag
  Total 2015 NPR Science Fiction & Fantasy recommendations: 57 books
  Enter the 'number' of the book you'd like to learn more about, or:
  'exit' to end program
  ==> Command:
  {% endhighlight %}

  And, end the program by entering the 'exit' command.

  {% highlight bash %}
  ==> Command: exit
  Exiting program...
  Thank you for checking out NPR's Book Concierge. Goodbye!
  {% endhighlight %}

Once I have built the CLI interface with stub information. I'm ready to connect the stub strings with <a name="make">real</a> objects.  This is where I build a separate class to create individual list object then I initiate a book objects to store all the book attributes.

## <a name="discover">List.rb</a>

## Book.rb

## <a name="program">Scrapper.rb</a>

### NPR website

+ couldn't scrape npr website
+ found web.archive.org
+ still need to figure out a way to scrape npr website
+ found NPR's Visual team's github (interesting find)
+ couldn't decipher NPR website's repo
+ found NPR API
+ more research needed

### Amazon.com website

+ tried a shortcut by scraping NPR's amazon links
+ then found amazon.com/dp
+ then found amazon.com/search

## Publish Gem

+ went smoothly with neighbor's help
+ came to the conclusion that it is scary and nerve wrecking when things go smoothly
+ better to see errors and fix them then to not see any errors - TDD
+ doesn't feel like we are learning when things just working

## Updating Gem

+ update files, update version
+ commit, push git repo
+ `bundle exec rake release`

# Breadth vs Depth

+ trying to add too many features before a fully working prototype
+ had to scale back and discipline myself to focus on shipping one working feature at a time

# Challenges

+ Scraping the invisible
+ Gem executable

# Conclusion

+ Felt good to have a good handle of Ruby to make progress in the CLI data gem.
+ Almost at every obstacle, able to look up resources, decipher quickly and implement into code to resolve the obstacle.
+ Felt the obsession to improve or add new feature to a working gem.
+ Found it more interesting to work on fellow student's project to figure out challenges together and create new feature together.
+ Learned so much about myself and also feel so empowering to have achieved this milestone.
