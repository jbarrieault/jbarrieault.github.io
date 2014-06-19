---
layout: post
title: "Expressive"
date: 2014-06-19 01:05:31 -0400
comments: true
categories: flatiron school, expressive code, ruby, programming, web development, coding
---
I don't know if you've heard, but there is a terrible rumor about programming going around. If you haven't heard it yet, you will soon. It's really making the rounds. And when you hear it, you'll be tempted to believe it and spread it yourself. But please, don't fall for it. You're better than that. I'm going to tell you the rumor, because I think you can handle it. But again, don't buy in. 
Ready? Okay then, here it is:

>"Programmers write code for computers."

Pretty awful, isn't it? I mean, this is a real atrocity! No? You don't think so? I think I know what you are thinking. On the surface it seems to be true and completely sensible. After all, the whole reason programming languages were invented was so we would have a way to tell computers to do stuff. You know, speak to them in a way they can understand. Be that as it may, programmers are **not**, I repeat **not** people who write code for computers. In actuality, **Programmers are people who create programs**. Think I am being overly dogmatic? Well I'm not. The difference is not a matter of mere semantics, but of an underlying understanding of what your goal as a developer really is. The side of this divide you fall on will dictate a great deal about the programs you create and the code you write to create them.

When writing code (as a programmer, developer, software engineer, or whatever you want to call yourself), it is very important for your computer, and other computers, to understands it. Yes, for sure. However, it is *even more* important for *people* to understand it. I'm seriously not making this up. Just look at this quote from the renowned [Hal Ableson](http://en.wikipedia.org/wiki/Hal_Abelson):

>"Programs must be written for people to read, and only incidentally for machines to execute."

Hopefully you believe me now that I pulled Ableson gun out. But you might still be wondering what this really means or has to do with the code you write. It's about writing expressive code. What is expressive code? Take a guess. It's code...that...is expressive. Yep, that's it. Expressive code is just code that is intentionally written to be easily understood by humans. I like to write in Ruby, which is a very expressive language. It is lacking in curly braces, semicolons, and boilerplate code other languages are known for. But just because Ruby is expressive and I write in Ruby does not mean I am writing expressively. It just means I have a head start. Expressive code can be written in any language, because it an approach to writing and organizing code that transcends the mere syntax of the language you are currently constrained to obey. 

Let me explain what I mean. We tend to think computers are rigid in their requirements and that people just have to put up with whatever code it takes to make a program run or a test pass, no matter how ugly or confusing to look at it may be. I won't say this is completely untrue. There is a level of syntactic precision computers demand in order to work (because they are stupid and they don't know any better). But in a sense, it is computers that are flexible and people who are limited in what code or syntax they can understand. You can write a program, or even a simple method, nearly endless ways. Your computer doesn't have a preference on how you write the code, as long as it works. People on the other hand, we have preferences. And we do care how a program it written. We like being able to quickly look at a method and be able to see what it does. Writing code that keeps this in mind is what it means to write expressive code. I think we have reached example time.

So let's look at some code. Say we have an array containing hashes representing bands:

```ruby
[ 
  {"The White Stripes" => {"The White Stripes" => "1999", "De Stijl" => "2000", "Elephant" => "2003", "Get behind Me Satan" => "2005", "Icky Thump" => "2007"} }, 
  {"Fleet Foxes" => {"Fleet Foxes" => 2008, "Helplessness Blues" => 2011}},
  {"Jonsi" => {"Go" => "2010"} } 
]
```

Say we want to print every album name to the screen. You could write it like this:

```ruby
a = [ 
      {"The White Stripes" => {"1999" => "The White Stripes", "2000" => "De Stijl", "2003" => "Elephant", "2005" => "Get behind Me Satan", "2007" => "Icky Thump"}}, 
      {"Fleet Foxes" => {"2008" => "Fleet Foxes", "2011" => "Helplessness Blues"}},
      {"Jonsi" => {"2010" => "Go"}} 
    ]

a.each do |v|
  v.each do |w, x|
    x.each do |y, z|
      puts z
    end
  end
end
``` 

To the computer, this is completely valid code and will output the desired results, which would be:

The White Stripes  
De Stijl  
Elephant  
Get behind Me Satan  
Icky Thump  
Fleet Foxes  
Helplessness Blues  
Go


But how would you feel if you were tasked to update/fix/optimize some code and you ran into that cryptic mess we just saw? Worse yet, what if you lacked the luxury of seeing the definition of the array being iterated over at all? Effectively leaving you with the following:

```ruby
a.each do |v|
  v.each do |w, x|
    x.each do |y, z|
      puts z
    end
  end
end
```

I would be completely in the dark if this was all I had to go on. All I would know from looking at the above code would be that some multi-dimentional collection was being iterated over and eventually an inner value is printed. This is nearly useless and will force me to stumbled around the source code files trying to figure out exactly what that collection is. And this is just a simple example. The more complex your objects and methods get, the more lost you and others will become when looking at your code. 

##Self Documenting Code (naming things)

So how could we write that procedure to be more expressive? There are a few important principles for writing expressive code. One of the most important ideas is called [self documenting code](http://en.wikipedia.org/wiki/Self-documenting). One key convention for self documenting code is giving variables meaningful and accurate names. Sound easy? Well actually, it can be pretty tough sometimes. You might be on a roll pumping out your code, not needing any help remembering what's what, and definitely not wanting to slow down just to think of what to name a variable. But it will come back to bite you and anyone who needs to work on the project if you don't take the extra set of seconds to come up with a decent name. Let's rewrite the previous example using simple, descriptive names for our variables:

```ruby
music_library = [ 
      {"The White Stripes" => {"1999" => "The White Stripes", "2000" => "De Stijl", "2003" => "Elephant", "2005" => "Get behind Me Satan", "2007" => "Icky Thump"}}, 
      {"Fleet Foxes" => {"2008" => "Fleet Foxes", "2011" => "Helplessness Blues"}},
      {"Jonsi" => {"2010" => "Go"}} 
    ]

music_library.each do |band|
  band.each do |name, albums|
    albums.each do |year, album|
      puts album
    end
  end
end
```

Wow! Now I can see what's going on! This is much more readable, and literally the only difference is the names of the variables. The computer doesn't care, but I sure do. I might not know exactly how music_library is structured if I don't know where it was defined, but at least I know that it is a music library. And in the first place, it was much easier to write the above code than the first version we looked at. I didn't have to keep track of the music list's structure in my head. One more thing, I should probably have wrapped that code into a method and given that a good name too. 

```ruby
def library_albums(music_library)
  music_library.each do |band|
    band.each do |name, albums|
      albums.each do |year, album|
        puts album
      end
    end
  end
end
```

There we go. Everything makes sense now. That is an example of self documenting code. If you are like me, you look at this example and think, "Yeah, I'm gonna start making my code more readable. It'll be great." However, minutes later you will find yourself taking shortcuts, sacrificing clarity to save a line of code or two. Then you start making excuses for it, like, "this is 3 lines shorter, so it must be more expressive." Or you might think about how impressed others will be when they see you chain six methods together on one line. And who doesn't want to be impressive? You don't, that's who.

There's a really great talk called [The Myth of the Genius Programmer](https://www.youtube.com/watch?v=0SARbwvhupQ) by a couple of guys from Google (Ben Collins-Sussman and Brian Fitzpatrick) in which they talk about some destructive habits programmers fall into in order to appear clever to their peers. The bottom line is that we like to look smart. The problem is that when we give our priority to making our code look smart over making our code easy to understand, we hinder our ability to collaborate with other developers. This hinders the project and our own continued growth. So always be on guard not to get carried away while refactoring your code. Refactor towards simplicity and clarity, not mere brevity. In other words, try to be *expressive*, not *impressive*.

There are many other practices for writing expressive code that I have not gone into here, such as the [Single Responsibility Principle](http://en.wikipedia.org/wiki/Single_responsibility_principle). I recommend [this blog post](https://robinwinslow.co.uk/2013/11/22/expressive-coding/) on the subject of expressive code. His examples are in JavaScript. I found it a very helpful place to start.

#tl;dr

Expressive code is code that is intentionally written to be easy for people to read and understand. One important aspect of expressive code is naming variables and methods descriptively and accurately. Remember, a program with the fewest (or most!) lines of code is not always the best. Don't try to make yourself look smart by making a program hard to read. Be expressive, not impressive.