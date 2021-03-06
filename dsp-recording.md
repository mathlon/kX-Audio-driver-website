# Direct Recording Guide

## Introduction

The 10k1 and 10k2-based audio cards support SPDIF digital inputs and outputs. It is widely 
known that the 10k1 and 10k2 chips operate at a fixed sampling rate, 48000 Hz. So, in order
to synchronize internal clocks with SPDIF In signals, the input stream is resampled to 48000
frequency (regardless of its original frequency). Moreover, if the input stream frequency is
already 48000, it is still resampled in order to avoid possible synchronization issues. That
is why it is theoretically impossible to record SPDIF input bit-to-bit (make an 'exact' copy
of the digital signal). The problem cannot be fixed for 10k1-based boards, however, the 10k2 
chip (used in Audigy and Audigy2 series of cards) has a special feature - Direct SPDIF recording.

## Detailed description

The 'Direct SPDIF Recording' is activated via kX Mixer (on the main page). Due to the nature 
of this recording method, the signal completely bypasses the DSP, which is why it is not 
affected by any uploaded effects or by the kX Mixer sliders and recording levels. After enabling
'Direct SPDIF Recording' no other recording sources are unavailable.
It is possible to choose which SPDIF input to record: Coaxial/Optical SPDIF, CD SPDIF etc. In
the present implementation it is possible to record analog I2S sources (Line2/Mic2, AUX2) in
'direct' mode, too. This feature is currently being tested since this aspect of hardware 
functionality has not been clearly defined.

Note that SPDIF inputs can transmit the signal at any sampling rate (44100, 48000, 96000 etc...),
so, it is up to user to choose the correct sampling rate in his/her audio application. The kX
driver won't try to autodetect the sampling rate. The sampling rate is, however, limited by the 
actual hardware capabilities. It should be possible to record at 96000 frequency on practically 
every 10k2-based board (such as Audigy1 and Audigy2). Also note that it might require up to 10
seconds for the SPDIF Input to synchronize to the incoming signal, if its sampling rate is more 
than 48000. If the signal is distorted or audio is muted, try unplugging and re-plugging the SPDIF cable.

## Conclusion

Direct SPDIF recording drammatically improves the recording quality of digital sources when the 
main goal is to make an 'exact' copy of the digital signal. The improvements include better 
frequency response and intermodulation. In the present implementation Direct SPDIF Recording is 
not supported for ASIO.
