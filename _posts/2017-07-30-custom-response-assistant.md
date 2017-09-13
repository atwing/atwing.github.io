---
modal-id: custom-response-assistant
date: 2017-07-30
header:
  overlay_image: /img/projects/teaser_custom_response.png
  overlay_color: 
project-date: July 2017
category: Home Automation
title: Custom audio response for Google Assistant
excerpt: Triggering Google Assistant on your own device without hotword detection does not give a trigger response. This entry intends to fix this by adding a custom audio response every time a conversation is started.
---

{% include toc title="Contents" icon="list" %}

Our custom [Google Assistant trigger]({{ site.baseurl }}/home%20automation/BT-control-assistant/) opened up many possibilities for starting a conversation with the Assistant. But without any display on the headless Raspberry Pi, it is hard to know whether the trigger has been registered and when we can start making our voice request.  
In this post we will provide the Google Assistant with a custom audio response. This can be anything from a beep tone, a spoken "Listening", "Yes Sir" to "Sorry buddy, not today!".  

The problem with playing an arbitrary audio file while using Google's gRPC API as in the [previous post]({{ site.baseurl }}/home%20automation/BT-control-assistant/), is that it blocks our audio output device so that other applications aren't able to access it while the streaming runs. One more or less inelegant solution would be to tap into this audio stream and push the frames of our custom audio response. Afterwards we release it for the Assistant to use as usual.

### Requirements
You can find the necessary files in this Git repository: [link](https://github.com/atwing/HomeAI-tutorial). It also contains scripts from the Bluetooth remote implementation which we will use as an example script to implement our custom response.

### Step 1: Extract frames from audio file
I will use the default beep sound from the Google Assistant on Google Home or Android devices, uploaded in the Git repo as **beep-response.wav**. We can handle WAVE files in Python using the **wave** module. Add `import wave` to the script to use it.

Note: When selecting a custom audio file, keep in mind that it has to have a sample rate of 16kHz. The stream used by the Assistant is configured sample at this rate.
{: .notice--info}

The file is first converted into a wave_read object from which we can extract the frames for later use:
```py
# load audio response file as a wave_read object
wavep = wave.open('beep-response.wav', 'rb')
# number of frames in audio response file
num_frames = wavep.getnframes()
# get frames from wav file
resp_samples = wavep.readframes(num_frames)
```  

The sequence of frames contained in **resp_samples** can be written directly onto the **conversation_stream** object in the sample script.

### Step 2: Play audio file
Before forwarding the frames we need to activate the audio stream which is a private member of the **conversation_stream** object, meaning we can't activate it directly. And here comes the inelegant part: the audio stream can be activated using the **start_recording()** function. We will hold the input channel with **stop_recording()**, start the output channel with **start_playback()** and are then able to write our frames onto the stream. Finally the stream is inactivated and released for the Assistant to use.

```py
stream = conversation_stream

# [...]

# announce listening phase with audio response
stream.start_recording() # activate audio stream
stream.start_playback()
stream.stop_recording()
stream.write(resp_frames) # write response frames to output stream
stream.stop_playback() # inactivate audio stream
```  

Add the lines before **assistant.converse()** is executed to get a response whenever the Assistant is about to recording your query.  
You can find my implementation in the file **pushtotalk_resp.py**.  
Whenever you trigger a request you should now hear your custom response first, before the Assistant starts recording with the announcement "Recording audio request".

<br><br>
If you have a better way of playing a custom response, I would love to know! Happy hacking and hopefully I will see you next time when we integrate IFTTT and Home Assistant to the system to run [shell commands via Google Assistant]({{ site.baseurl }}/home%20automation/shell-commands-assistant/).
