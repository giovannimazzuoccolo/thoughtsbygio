---
title: "Being Kind to AI Will Consume More Tokens?"
description: "Exploring whether adding politeness and kindness to AI prompts actually increases token usage and costs, and why it might be worth it anyway."
pubDate: "Oct 23 2024"
heroImage: "../../assets/ai-kindness-hero.jpg"
---

So here's something I've been thinking about lately. We're all chatting with AI assistants now, and I've noticed people have wildly different approaches. Some folks are super direct and commanding (I live in The Netherlands, I would call it the "Dutch directness") while others are adding "please" and "thank you". Does being polite to AI actually cost us more in tokens?

The answer is yes, it does. Adding a few polite words to your prompts might cost you an extra few cents per month unless you're absolutely hammering these APIs all day long.

Before we dive into this, let's have a quick review on how this whole token thing works. When you send a message to an AI, it doesn't just read your words like a human would. Instead, it breaks everything down into tokens, which are basically chunks of text that could be whole words, parts of words, or even just punctuation marks. Every single character you type gets converted into these tokens, and that's what the AI actually processes. The AI then analyzes all these tokens to understand what you're asking for, picking up on patterns, context, and meaning from the way these tokens are arranged together. For example:

```
Debug this (2 tokens)
```

versus

```
Please debug this function and explain me the results (9 tokens)
```

Same basic request, but one uses more than four times the tokens of the other.

## Why Being Nice Might Actually Help You

Here's the thing though, and this is where it gets really interesting. Being polite to AI might actually make your prompts better, not because the AI has feelings or anything, but because it changes how you approach the whole conversation.

Think about it. When you're being polite, you're naturally being more thoughtful about what you're asking for. You're not just barking commands, you're actually explaining what you need and why. That extra context and consideration often leads to way better responses, which means you're less likely to need follow-up questions to clarify what you meant.

## The Training Data Connection

There's another angle to consider here. These AI models learned from massive amounts of human text, and a lot of that text includes polite, conversational language. While the AI doesn't actually care if you're nice to it, it has learned patterns where polite requests often come with more context and lead to more detailed, helpful responses.

It's not that the AI is rewarding your politeness, it's more that polite language tends to be associated with clearer communication in the training data. When you ask nicely, you're tapping into those learned patterns of effective human communication.

But here's something worth considering: your conversations with AI don't just disappear into the void. Many AI systems use interactions to improve their models over time. This means that when you're polite and kind in your prompts, you're actually contributing to making AI more polite and helpful in the future. If millions of people start being more courteous with AI, future versions will learn that this is how humans naturally communicate.

This becomes especially important when we think about younger generations who are growing up with AI as a normal part of their lives. Kids and teenagers are learning how to interact with these systems right now, and the patterns they establish could shape how AI responds for years to come. If we normalize polite, respectful communication with AI, we're essentially teaching future AI models that this is the standard way humans like to interact. On the flip side, if everyone starts being rude and demanding, that becomes the learned behavior pattern too.

## When Every Token Counts

Now, if you're building applications that make thousands of API calls or you're working with a really tight budget, then yeah, every token matters. In those cases, you might want to strip out the pleasantries and focus purely on efficiency. But for most of us just using these tools for daily tasks, the cost difference is so small it's barely worth thinking about.

The real question isn't whether being kind costs more tokens, it's whether that tiny extra cost is worth the potential benefits of clearer communication and better responses. For me, it usually is.

## My Take on the Whole Thing

Look, being kind to AI will technically use more tokens, but we're talking about such a small amount that it's almost irrelevant for most people. What's more interesting is that polite language often leads to better prompts, which can actually save you tokens in the long run by getting you the right answer faster.

Whether you want to say "please" to your AI assistant is totally up to you. The AI doesn't care either way, but you might find that being conversational and polite helps you communicate more effectively. And if that's the case, those extra few tokens are probably worth it.
