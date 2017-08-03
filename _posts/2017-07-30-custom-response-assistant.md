---
modal-id: custom-response-assistant
date: 2017-07-30
img:
project-date: July 2017
category: Home Automation
title: Custom audio response for Google Assistant
excerpt: Triggering Google Assistant on your own device without hotword detection does not give a trigger response. This entry intends to fix this by adding a custom audio response every time a conversation is started.
---

{% include toc title="Contents" icon="list" %}

Our custom [Google Assistant trigger]({{ site.baseurl }}/home%20automation/BT-control-assistant/) opened up many possibilities for starting a conversation with the Assistant. But without any display on the headless Raspberry Pi, it is hard to know whether the trigger has been registered and when we can start making our voice request.  
In this post we will provide the Google Assistant with a custom audio response. This can be anything from a beep tone, a spoken "Listening", "Yes Sir" to "Sorry buddy, not today!".  

The problem with playing an arbitrary audio file while using Google's gRPC API as in the [previous post]({{ site.baseurl }}/home%20automation/BT-control-assistant/), is that it blocks our audio output device so that other applications aren't able to access it while the streaming runs. One more or less inelegant solution would be to tap into this audio stream and push the frames of our custom audio response. Afterwards we release it for the Assistant to use as usual.

[More coming soon!]

<br><br>
