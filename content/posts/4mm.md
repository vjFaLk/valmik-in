---
title: "4mm"
date: 2016-03-01T07:38:33+05:30
draft: false
featuredImg: ""
tags: 
  - Story
  - Debugging
  - Freelance
  - IHateBarcodes
---

I had a client from New Zealand whose business depended on shipping packages to his customers every week. Packages need a shipping label with a barcode on so they can be scanned and picked up.

For some reason, the courier would take several tries to get each package scanned. My client asked me if I could have a look into why.

It looked like a typical barcode, black and white lines in a straight line, so it should work…right? The codebase wasn’t my work. I didn’t really know where to start. But I sifted through a bunch of (poorly written) PHP code to find the parts that did the work. But I couldn’t find anything that was obviously off.

We did a video call with someone from the courier company, Michael, who sent me several (8!) PDF documents regarding specific details about labels, barcodes and what not. I went through those documents and checked if our barcode was adhering to the quality standards and format requirements that the courier company was. They were. (Well, at least that's what I thought.)

We did a video call with an experienced PHP developer who was an expert at dealing with all things courier related. He couldn’t find anything wrong with the barcode.

I scanned the barcode with my phone, using a barcode scanning app (installed since the beginning of time but never really used), and it…worked? *What*. Also, it turned out, some of the newer scanners were able to scan the barcodes perfectly but the old ones were a hit or miss. *What*. So, we have a somewhat working barcode…But we needed it to work with older scanners.

Over the course of almost two weeks, I made several changes to get the barcode to work, repeatedly going through all the reference documents and kept sending them to Michael. He couldn’t scan them.

We were all at the end of our wits, utterly clueless as to why the damn barcode wouldn’t scan.

On the day before shipping, I scrapped all the changes I had made apart from a single change. Because at least that old barcode worked sometimes, right? After that, I went to sleep.

I woke up the next day to several messages from my client in glorious ALL CAPS stating that somehow all the barcodes are now working instantly with any scanner. I was more confused than happy. What in the world could’ve fixed it?

You see, I had changed the width of the shipping label by 4mm (170mm to 174mm) to match the exact width mentioned in the documents (without any intent to fix the barcode; what's 4mm going to change, right?). One character. That’s all that was needed. That’s what fixed the issue.

Weeks of work to change one character.

One character to fix the issue.