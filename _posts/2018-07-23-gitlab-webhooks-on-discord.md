---
layout: post
title: "Gitlab Webhooks on dicord"
category: blog
tags: programming
---

#movingtogitlab:tm:

First published [here](https://programming.im/guides/14) on June 10, 2018.
<!--more-->

Everyone is [#movingtogitLab](https://about.gitlab.com/2018/06/03/movingtogitlab/), and no matter what Microsoft fan boys tell you,
it is for totally legitimate reasons. Moving to GitLab is easy, it's literally
two clicks. (This post is **NOT** sponsored by GitLab.) 

Merely moving the repositories isn't enough to recreate the same workflow you
had before Microsoft pushed you away from GitHub. You'll want to re-setup your
integrations with all these awesome services you were using back on GitHub. (LOL
jk gh has no integrations with anything whatsoever :^), this is a fact.)

While GitLab offers way more integrations than GitHub, some of them might not be
that obvious to set up. Discord webhooks, for example, are tricky to get working
with GitLab. Here's how to get up and running with them.

To create a GitLab webhook for a discord channel, you can follow the same
procedure laid out on the [Discord help Center](https://support.discordapp.com/hc/en-us/articles/228383668-Intro-to-Webhooks), and in the [gitlab docs](https://docs.gitlab.com/ee/user/project/integrations/webhooks.html). But,
*because there is a but*, this won't work. And you can verify this by creating
the webhook and then trying to test it with the test button from your GitLab
repository. You'll either have an error about blank messages not allowed or
will be clearly told that a required field is missing. In short, the GitLab
webhooks are not supported by Discord and vice-versa. But don't you worry,
there's a workaround.

While you're on the integration page on GitLab, scroll all the way down to
`Slack notification`. You can learn more about these services [here](https://docs.gitlab.com/ee/user/project/integrations/project_services.html) by the way.
In the `Slack notifications` service configuration page, start by checking all
the events you'd like to be notified of on Discord, it's really the same process
for GitHub. Don't bother with the channel name field, it won't change anything,
unless you're using Slack. 

Next, at the bottom of the page, paste the webhook link you
got from Discord. **Important!!** Add `/slack` **Important!!** at the end of the
webhook URL you got from Discord. 

GitLab also gives you the ability to name your webhook however you like, how
sweet (<sup>o</sup>^)! You can also set a profile picture for it from Discord and it won't
be overriden by some generic octopus :^).

Lastly check wether or not you want to be notified only for broken pipelines 
(pipelines are awesome by the way) and if you'd like to be notified only of events
from the default branch of your project.

Now, go ahead and click `Test and save changes`. Check in your Discord channel,
you should have received a message from the webhook with the content
of one of the recent actions (push, merge, &#x2026;) on your project. 

It's that simple! Enjoy!

