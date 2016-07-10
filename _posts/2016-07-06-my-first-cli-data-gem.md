---
layout: post
title: My First CLI Data Gem
navi_title: Blog Post
date: 2016-07-06 12:00:00 -0500
excerpt_separator: <!--more-->
---

So it finally happened.  I've created and published my first CLI data gem on [RubyGems.org](https://rubygems.org/gems/npr_best_books).  Here's how I did it and the [Github repo](https://github.com/beingy/npr-best-books-cli-gem) for reference.<!--more-->

I've also created my first walk-through video to demo how my CLI data gem works. Please see below.  Enjoy.

*Insert Youtube walk-through here*

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

## Scope & Inspiration (Step 1a.)

The point of the CLI data gem basically want us to be experimenting with extracting data from an external source and interact with it in real time from a command line interface (aka CLI) in a text-only user interface.  The scope also wanted us to drill down at least one level to pull additional details from the initial data we gathered.

Sounds fun!  What's next?  Where do I want to "scrape" information from and display it in a useful manner and then provide additional information upon request?

*Being's mind at work*

I don't read as much as I think about reading.  Ever since I've started learning to code, I want to think less and do more so I have been reading a lot of science fiction books one after another on my hour long commute to and from Flatiron School campus in the Financial District.  And, for the longest time I always been looking for interesting books to read.  

Keeping my streak of reading daily on my commute, I started to track the books I read on [GoodReads.com](https://www.goodreads.com/user/show/53599856-being) so naturally I thought GoodReads was a great place to start.  I started checking out GoodReads's overwhelming lists of book recommendations and quickly shied away from attempting on the monumental task. *It was much later on while working on the CLI data gem that I realized I could have still scraped GoodReads and I still might do it as a challenge as long I have narrowed down to a specific list.*

My next target was [NPR's Book Concierge](http://apps.npr.org/best-books-2015/) website that featured recent year's book reviews in various genres and provides a single list of book recommendations from book critics, journalists or notable curators year to year.  Bingo!

## <a name ="imagine">Imagine a CLI interface</a> (Step 1b.)
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

#### Phrase 2 (Amazon)
+ A book has an ISBN/ISBN13
+ A book has a publisher
+ A book has a number of pages
+ A book has a type (Hardcover or Paperback)
+ A book has an Amazon rating
+ A book has an Amazon price

I know I definitely want to try getting Amazon's ratings to get a sense of each boo

# Development

## <a name="structure">Getting started</a> (Step 2)

How do I get started?

## Setup Gem via Bundle Init

## GitHub Version Control

## <a name="cli">CLI</a> interface (Step 3-5)

At this point, I would stub strings to stub objects to actual scraping data

Build list objects then add book objects

- A command line interface to access NPR Best Books by year
(Step 3)
user types npr-best-books

<a name="force"></a> show a list of NPR Best Books for Science Fiction & Fantasy from the most recent year.

<a name="stub">(Step 4)</a>
<a name="make">(Step 5)</a>

## <a name="discover">List.rb</a> (Step 7 Part 1)

## Book.rb (Step 7 Part 2)

## <a name="program">Scrapper.rb</a> (Step 8)

### NPR website

couldn't scrape npr website
found web.archive.org
still need to figure out a way to scrape npr website
found NPR's Visual team's github (interesting find)
couldn't decipher NPR website's repo
found NPR API
more research needed

### Amazon.com website

tried a shortcut by scraping NPR's amazon links
then found amazon.com/dp
then found amazon.com/search

## Publish Gem

went smoothly with neighbor's help
came to the conclusion that it is scary and nerve wrecking when things go smoothly
better to see errors and fix them then to not see any errors - TDD
doesn't feel like we are learning when things just working

## Updating Gem

update files, update version
commit, push git repo
bundle exec rake release

# Breadth vs Depth

trying to add too many features before a fully working prototype
had to scale back and discipline myself to focus on shipping one working feature at a time

# Challenges

Scraping the invisible
Gem executable

# Walk-through Demo

2-3 minute walkthrough of Gem
installation
run program
try features
talk about interesting little details
exit and thank you

# Conclusion

Felt good to have a good handle of Ruby to make progress in the CLI data gem.
Almost at every obstacle, able to look up resources, decipher quickly and implement into code to resolve the obstacle.
Felt the obsession to improve or add new feature to a working gem.
Found it more interesting to work on fellow student's project to figure out challenges together and create new feature together.
Learned so much about myself and also feel so empowering to have achieved this milestone.
