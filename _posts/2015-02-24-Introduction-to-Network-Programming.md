---
layout: post
title: "Introduction to Network Programming"
description: "Low level languages like C use data structures like structs
to manually create packets and then use
operating system commands under the hood to communicate these packets to other
systems"
category: "computer science"
tags: [computer science]
---
{% include JB/setup %}

<h1>How do http request work under the hood?</h1>
<p>
Recently, I was using <a href="http://nodejs.org/api/http.html">Node's http
library</a> for a project when I became very intrigued
as to exactly how http worked under the hood. 
I wanted to understand how writing code could translate into communicating with
other networks. Obviously Node's http library has methods which make this easy,
but I wanted to know how those worked on a low level. To get to the bottom of
this I decided to do a stack track of an outbound server response using Node debugger.  I traced the http response from my Node server, but I
could not find any point where the data in my outbound response was actually
transmitted across the network. It appeared as though
under the hood Node's http library just manipulates the data by breaking it down
into smaller and smaller packets until eventually it uses some external library
to ship it off. Reading source code did not answer by underlying questions, I
decided to ask the programming community.</p>


<p>When I went to ask the community how it is possible to writing code could 
translate into a request over a network, the most common response I received is
that this is the result of a C
library. There are libraries written in C and other low level languages which
abstract these network details away. My question became, "but how are those libraries
written? I became obsessed with the question: 'How does writing pure vanilla
code create a request over the internet ?'. I searched
around for a bit before finally discovering <a
href="http://beej.us/guide/bgnet/output/html/singlepage/bgnet.html">Beej's Guide
to Network Programming</a> and then it all came together for me.
</p>

<h1>A Brief Introduction to Network Programming</h1>
<p>It turns out that low level languages like C use data structures like structs
to manually create packets and then use
operating system commands under the hood to communicate these packets to other
systems. I will spend the rest of this article noting the structures and
architecture of this network programming that is usually abstracted away. 

<h3>Stream Sockets</h3>
<ul>
  <li>Reliable two way communicative streams</li>
  <li>Application of Stream Sockets is called <i>Transmission Control Protocol</i> (TCP)</li>
  <li>Uses TCP which ensures data arrives sequentially and error-free</li>
  <li>Http uses TCP and thus also stream sockets</li>
  <li>Example Uses: browsing websites and sending email</li>
  <li>Primary purpose of TCP is data integrity</li>
</ul>

<h3>DataGrams sockets</h3>
<ul>
  <li>Fast unidirectional communication</li>
  <li>Application of DataGram Sockets is called <i>User Datagram Protocol</i> (UDP)</li>
  <li>Datagram sockets do not require an open connection as is the
  case with tcp, this makes them <i>connectionless</i></li> 
  <li>Example Uses: streaming video games, audio, and videos.</li>
  <li>Primary purpose of UDP is speed</li>
</ul>
<img src="http://wand.net.nz/pubs/19/html/img1.gif"></img>


<h3>Conclusion</h3>
<p><a href="http://inst.eecs.berkeley.edu/~ee22/fa07/projects/p2files/packet_parser.c">C
uses structs to create packets which use these sockets.</a> It then uses
operating system network commands under the hood to communicate these packets
to other systems.</p>

<p>In conclusion, I feel satisfied with the results of my inquiry. This blog
posts was more verbose than I would ordinarily prefer, but I felt understanding
my creative process in this adventure was just as important as the end result
which I achieved. This highlights what programming is really about to me- the
creative process, alert focus, and personal mastery.</p>

<blockquote>We are all in search of feeling more connected to reality—to other
people, the times we live in, the natural world, our character, and our own
uniqueness. Our culture increasingly tends to separate us from these realities
in various ways. We indulge in drugs or alcohol, or engage in dangerous sports
or risky behavior, just to wake ourselves up from the sleep of our daily
existence and feel a heightened sense of connection to reality. In the end,
however, the most satisfying and powerful way to feel this connection is through
creative activity. Engaged in the creative process we feel more alive than ever,
because we are making something and not merely consuming, Masters of the small
reality we create. In doing this work, we are in fact creating
ourselves.</blockquote>
― Robert Greene, Mastery

