---
layout: posts
title:  "Week 10: Coding Period"
date:   2022-08-27 21:55:00 +0530
categories: gsoc
---

This week I looked into MultiProcessing Conditions and finished the video of the FSM. 

## Video

After consulting with Jose Maria Canas, I added extra slides and description to the video. Finally I capped it off by adding subtitles and background music. As my video editing skills have improved somewhat, this video was pretty good :).

<iframe width="560" height="315" src="https://www.youtube.com/embed/AtYmeD9ojUo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Conditions

The next aspect of this week was the focus on Multiprocessing Conditions for the FSM implementation. After trawling through many examples and Python's Documentation, I got the hang of how Conditions were implemented. 

Subsequently I used them through Visual Circuit to implement the FSM. Using Conditions and a shared Value variable, I was able to implement a perfectly working FSM with virtually no changes to the code of the original Visual Circuit program.

The only the differences were as follows:
Adding Value and Condition to the `main.py` file:
```python
fsm = Value('i', 1)
condition = Condition()
.
.
processes.append(
            multiprocessing.Process(target=method, args=(inputs, outputs, parameters, fsm, condition, Synchronise(1 / (freq if freq != 0 else 30))))
        )
```  

This made me change the template of the blocks as follows:
```python
def main(inputs, outputs, parameters, fsm, condition, synchronise):
```

Finally an example of a block made using Conditions:
```python
def main(inputs, outputs, parameters, fsm, condition, synchronise):
    IS_INITIAL = True

    with condition:
        while True:
            if fsm.value == 1 or IS_INITIAL:
                IS_INITIAL = False
                # n = spiral(motors, bumper)
                # inputs.enabled = False
                print("Block 1 is executing ...")
                sleep(1)
                outputs.share_number('o', 2)
                fsm.value = 2
                condition.notify_all()
            else:
                condition.wait()
            synchronise()
```

Note that the above block was made as a test for how the Conditions worked together with `sleep` statements