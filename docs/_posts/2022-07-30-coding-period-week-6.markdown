---
layout: posts
title:  "Week 6: Coding Period"
date:   2022-07-30 23:55:00 +0530
categories: gsoc
---

This week was quite hectic for me. My college started offline after a while, due to travelling and a few other events the time I could spend on Visual Circuit was reduced to a certain exent.

Still, I managed to make some progress on last week's goals.

## FSM

I continued work on the FSM, I realized that the old block model I was using was unsustainable. This was due to a flaw in which all of the states were not updated, i.e. when the control moved from block 0 -> block 1 -> block 2 the state changes from 0 -> 1 -> 2. However block 1 will keep supplying state 1 to block 2 even though block 2 supplies 0 to block 0, this cause block 2 to repeatedly execute.

To fix this I switched to a Master-Controller relationship between the blocks as suggessted by my mentors last week. This involved having one block just to oversee the state and control the other blocks, the diagram looked something like this:
![Block Diagram Master-Controller]()

After this implementation I was able to get the Vacuum Cleaner implementation working the way it was intended. However there were certain cases in which it showed erratic behavior still. I showed it to my mentors and the conclusion seemed to be that the multiprocessing aspect of the application was causing some unexpected behavior. To fix this I suggested having a lock for the process what was currently being executed, however we did not come to a fixed conclusion about this issue.

## Documentation

Last week I had found [pdoc](https://pdoc.dev/) as a useful tool for documenting the application. This week I extended on last week's work by writing a simple Python script to extract all the json data from the block files, store them as python files and then run pdoc on them to generate some rudimentary documentation.

The next step for this was to adapt the tool to work according to our needs. That part will be worked on next week. The problem with the json implementation and custom block type work meant that this will require some rewriting of the code of `pdoc` itself.
Perhaps, not 100% sure about it yet.

## General Bugs

While giving a demo of some blocks I found that the Threshold block was incorrectly saved in the Tool, that will be fixed in a PR soon. Aside from that I identified what was causing the bug of the blocks opening with very small sizes. Apparently while saving the blocks their size was saved incorrectly. By editing these values in the JSON I was able to restore them to a normal size. This meant that would open in the correct size by default and the user would not have to spend time trying to re-size them.

![Example of a shrunken block]()


On an unrelated note, the Mid-Term evaluations of GSoC were this week. Quite happy that the project is on track!

## Issues
No new Issues were raised this week
## Pull Requests
No new Pull Requests were issued this week however some corrections and updates were made on already active ones from the previous week.