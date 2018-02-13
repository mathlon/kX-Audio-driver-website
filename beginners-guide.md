# kX Guide for Beginners

The kX Audio driver was developed for soundcards based on the Emu10k1 and Emu10k2 chips, such as the SBLive, Audigy and other cards. These Emu10kx chips are actually Digital Sound Processors (DSP). If you look at the DSP part of the kX Audio Driver, you can in fact edit the properties and behaviour of the chip on your sound card, by modifying routings, loading and tweaking effects and so on.

To explain this in a bit more detail, let's first look at the main parts of the kX DSP window. The best way to describe this is to imagine it as a kind of rack, with different input and output devices and effect devices, all connected by (very high grade) audio cables. The "devices" you see in the kX DSP window all have inputs (on the left) or outputs (on the right), or both, and are connected to each other with virtual audio cables (the blue lines).

Apart from the various plugin effects, there are 4 distinct "I/O" devices in the DSP window. These are the FXbus (2 if you have an 10k2-based card), the Prolog, the Epilog and the (x)Routing device. Let's explore these four in more detail, then we'll have a look at ASIO routing and wrap-up with a review of the kX Routing Window.

# 1. The FXBus

The FXbus has 16 outputs (or 32 for 10k2-based boards, and 64 if an additional 'FXBus2' effect is uploaded) for audio streams generated by software running on your PC ( such as an mp3 player, sound from a MIDI WaveTable synthesizer, or from one of the ASIO outputs). All audio data you generate, will be found on this device.

# 2. The Prolog

The prolog outputs any audio data originating from OUTSIDE your PC, such as the Digital Optical In on the LiveDrive, or the Digital CD (CDSPDIF) Connector on the card itself. One special output of the prolog device, which is the cause of much confusion among new kX driver users, is the AC97 output.

The 10k1 and 10k2 chips are digital chips (yes purists, not all chips are digital :-), and so they cannot accept analog input directly . On the Live! (Audigy) card, there is another chip responsible for this - the AC97 codec. This chip connects all of the analog inputs on the Live! board itself (with the exception of the LiveDrive inputs), mixes them, and feeds them into the Emu10kX. This codec is responsible for the LineIn and MicIn of the card itself, and the CD Analog In (but not CD Digital), among others. You can control this codec with the AC97 part of the kX mixer, remembering that the AC97 line on the Prolog is where the audio data emerges (the Prolog is also the place to find all of the other inputs on the card and on the LiveDrive). Note that the LiveDrive uses high-quality ADC (analog to digital converters) which are generally superior to AC-97 codecs (the E-mu APS and Audigy2 Platinum Ex don't have AC97 codecs at all).

# 3. The Epilog

The Epilog device is where all data eventually output. It consists out of 2 parts; the "real" ('physical') outputs, and the "sampler" (e.g. ASIO) outputs. The real outputs simply reflect all of the physical outputs (both analog and digital) on the Emu10kX chip. Note that the Emu10kX is capable of 4 stereo digital outputs (yes, the original Live!, and even the 512 PCI, are all 7.1 cards). In order to take advantage of this fact without using a LiveDrive one can use the "AUD_EXT" connectors found on most 10kx cards (although some special knowledge and experience is generally required) .

On most 10kX boards, the "front" channel analog output is generated by the AC97 codec whereas the rear channel is done by an I2S codec. For this reason (I2S output is generally superior to AC97 output), kX Audio Driver swaps the 'Front' and 'Rear' connections by default. Note that in the case of Audigy and Audigy2 boards, an I2S codec is used for front output, and the AC97 codec is used for recording from onboard analog connectors only. However, it is still recommended to swap the Front and Rear connections because the output signals from the AC97 codec (even muted) are still connected to the 'Front' output of the card (and this impacts sound quality).

The best way to understand all of this, and to take advantage of it, is to not see the 10k1 and 10k2-based cards as audio cards with front and rear outputs and all, but simply as a 4 stereo channel output chips (which they actually are). Nobody tells you that you MUST use the "green" connector for your front speakers; you can just as well use it for your headphone output, and use the "black" (rear) connector as the feed to an audio system (in a club, use the green connector for headphone, black for the house audio feed, and start DJ-ing with 2 separate audio channels). Why use the black for the house audio system? Simple - the black (rear) channel uses the I2S codec, and thus produces better sound... and the audience deserves the best :-).

The second part of the Epilog is the part with the recording/sampler outputs. These outputs (RecL/R and the 16 ASIO recording channels) are used to feed your PC with audio streams. If you output to, for instance, the RecL/R ports, you can record/sample the audio to hard disk by using the standard windows recorder. You can use the 16 ASIO channels, to sample data to, for instance, Cubase, OR use them to feed data into SpinAudio/SoundDT's effect processors. These ports are basically your input connections to your applications (as opposed to the FXbus, which is the output of your applications)

# 4. Routing

Thinking back to the imagined "rack" setup, it should already be clear what the Routing device is. It's the central mixer part. The Routing device mixes the standard outputs of the FXBus and Prolog to the standard inputs of the Epilog, using the settings in the kX mixer control panel (i.e. the sliders). It also has two groups of special FX inputs, which are used to add special effects to the sound. Typically however, the router sends these 2 special FX mixes only to the real output channels, and not to the recording channels. Note that you can tweak the recording level of inserted effects via kX Mixer's 'Rec' page.

BUT (and this is the power of kX), you don't have to use any of this! You can make your very own DSP setup, or different setups for different needs, which you can save and restore. For instance, plug your guitar into your LiveDrive's LineIn2. Clear the whole DSP window, and load only the pProlog and Epilog (found with the "default" effects on the effects insert menu). Connect the LineIn2 to the front speakers, and that's it - directly routed. Add another 'line' from the same LineIn2 to the RecL/R, and you can record it just as well. Maybe add a nice EQ or Compressor effect in between somewhere - you get the idea!

# 5. ASIO Routing

ASIO is the name of a driver "API" made by Steinberg, for the purpose allowing drivers to achieve lower latency. This means that you can have your computer process audio data (coming, for instance, from some software on your PC, or an input on your sound card, and outputting to your sound system), all with latencies as low as near realtime. So when striking notes on a guitar, effects can be added to the signal in almost realtime, and sent to your audio set.

The kX driver's ASIO support allows audio to stream through 16 input and output channels with latency as low as 2.66 ms on a fast and well-tuned system, for both recording and playback.

# ASIO Inputs

We've already explained where the ASIO inputs are found - 16 channels on the Epilog), route anything to there, and you can use the ASIO inputs in any application, to monitor, add effects, sample to hard drive, or output on the same ASIO drivers - or to any other output for that matter, but then you won't have the advantage of low latency which is the whole point of ASIO).

# ASIO Outputs

You have 16 ASIO outputs. By default, these 16 channels are mapped 1-on-1 on the FX bus, so the 1st ASIO channel outputs on the 1st channel of the FX bus (actually, FXBus #0). So, going back to our guitar setup, connect the LineIn2 on the Prolog to a set of ASIO recording channels, say the last two (these are suggested only because there is a small problem with SB006x cards not being able to use the 2nd and 3rd ASIO recording lines - see our FAQ for more details). You now have your guitar on the last 2 ASIO channels. Fire up SpinAudio to add some effects - your input will be the last 2 ASIO channels. Thinking back of the rack, you now have to get the output of SpinAudio back into the DSP in order to connect to some sort of real output (as in for example , our "front + recorder setup"). In Spin Audio, output to the first 2 ASIO channels, to get the signal on the first 2 outputs on the FX bus. Now, draw some virtual cables to the front speakers in the kX DSP window (and to the recorder again maybe, or to another ASIO recorder. You can have as many connections you like, but keep in mind that every "connection" to and from the DSP, using the ASIO In and Out channels, adds latency (note that the connections in the kX DSP do not affect the latency at all - you can have as many asyou wish). Add and enable the effects in SpinAudio; start playing, and you've just completed your first ASIO routing with custom effects! :-)

# 6. The kX Routing Window

New users sometimes find the kX Routing Window to be confusing, in part because it has nothing to do with the DSP Routing device and everything to do with the FXBus. If you look at the routing window, you will see all of the software generated outputs, in a tree list on the left. You have Wave 0/1, 4/5, 6/7 and 8/9 - these correspond to the 4 wave out devices and their names refer to the "standard" FX routing bus setup 4/5, 6/7 and 8/9 are essentially copies of the DirectSound/AC3, Front/Rear and Center/Sub channels with 0/1 being the "standard" wave out. You will also find the AC-3 (and DirectSound, as mentioned above) outputs, the 2 synths, and the ASIO outputs.

How does this relate to the FXBus?

Well, the FXbus has its own internal routing/mixing and all of the software outputs are mapped to one of the FXbus outputs. Normally, stereo wave pair 0/1 is routed to channels 0 and 1 (and also to 13 and 14 for effects). The ASIO Outputs are normally mapped 1-on-1 to the FXbus (channel 1 to FXbus 1), the synths to FX 2 and 3, etc., etc. (check the kX help file for a complete routing table). You may change any of these settings, but the defaults are typically fine for most purposes An example of a special setup would be the addition of multiple mixed effects to specific outputs (similar to the standard Reverb/Chorus on channels 13/14).

So: that concludes our overview of the workings of kX and ASIO - good luck with the drivers and the DSP, and experiment a lot :-) that's the best way to learn!

 written by Mata Hari
 (minor corrections by kX Team)