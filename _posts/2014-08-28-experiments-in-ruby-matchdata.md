---
layout: post
title: "Experiments with Ruby Matchdata"
description: "Messing with a unique Ruby Sasquatch"
category: Ruby
tags: [Ruby, MatchData, RegExp]
---
{% include JB/setup %}

I've been on the interview circuit of late -- as stressful as that can be, I feel like I've learned a lot through the wide array of interesting challenges that have been dropped on me. One of the cooler ones involved using a regular expression to take a MadLib, number the fields (and subsequently to fill in the verbs, adjectives and nouns of said MadLib). Initially the text just had parts of speech denoted inside of brackets like so: {verb}.

So this was an interesting new issue -- I've never had to match and replace that quantity of items in one passage. I also haven't needed as much information from a pattern match... ever.

The first step wasn't so tough after a bit of creative google-ing -- I built an enumerator to catch all the matchdata in an array. Like so: 

#### original_text.to_enum(:scan, /\{(.*?)\}/).map { Regexp.last_match }

This gave me a new array of each last_match via RegExp's last_match class method (obvi) via my old friend #scan. Once you have that data there are a ton of built in match variables and methods to make your life easier which we're going to go over now:

#### Instance methods:

##### hypothetical_match_data_object.captures 
=> Gives you the actual matched string -- so in this case "verb" or "noun" -- if you have one match it's also stored in the global variable $+

##### hypothetical_match_data_object.begin(0)
=> Gives you the starting position of the first character in the matched string. The argument allows you to offset that by a character. No idea why, but if you want to you can. When used with insert (which can take character position as an initial argument) you can do some nifty stuff here.

##### hypothetical_match_data_object.to_s
=> Gives you the full match so in this case "{verb}" or "{noun}" -- if you have one match it's also stored in the global variable $&

##### hypothetical_match_data_object.end(0)
=> Gives the position of the last character in the matched string. Once again, the argument allows you to offset that by a character. No idea why, but if you want to knock yourself out. 

#### Other potentially useful Matchdata global variables / instance methods: 

##### $` => Gives you the full string prior to match. #pre_match does the same thing as an instance method.

##### $' => Gives you the full string after the match. #post_match does the same thing as an instance method. 

##### $1 - $9 => Gives you the content of previous successful pattern matches.


Preeeeety kewl, eh? 

