![[Pasted image 20240402190538.png]]
The important take-away here is that quick changes in time domain result in many frequencies occurring.

Quick changes in time domain result in spikes in frequency domain 
![[Pasted image 20240402190721.png]]

#### Properties of Time-Frequency transform:
1. **Linearity**
   ![[Pasted image 20240402191455.png]]
2. **Frequency shift**
   ![[Pasted image 20240402191524.png]]
   (Take signal in time domain and multiply it by a sine wave shifts X(f) in frequency domain)
3. **Scale in time**
   ![[Pasted image 20240402192223.png]]
   (shrinks or expands the signal on time axis, thus changing the datarate. more dense signal needs more bandwidth)
4. **Convolution in time**
   ![[Pasted image 20240402192641.png]]
   (Convolution it time is multiplication of 2 signals in frequency domain. Convolution in time domain is how you can apply a mask to only pass some frequencies in freq domain)
5. Convolution in Frequency
   ![[Pasted image 20240402193017.png]]
   (reverse of convolution in time)

Output of FFT:
![[Pasted image 20240402214723.png]]
If sample rate fs = 1 MHz, see freq up to 0.5 MHz

#### FFT Shift
to re-arrange the outputs of x axis in freq domain
![[Pasted image 20240402220726.png]]
```Python
S = np.fft.fftshift(np.fft.fft(s))
```


#### Windowing
![[Pasted image 20240402221835.png]]
Use a window to make the function sample taper off to zero at the ends. This is so there be no sudden changes (sudden changes result in many frequencies), when the function is looped back together (fft treats the function as indefinite, where it loops back at the end)

#### FFT Size = always order of 2

### IQ Sampling
#### Signal Equation
![[Pasted image 20240409181529.png]]

#### Downconversion
Center the signal at 0 Hz DC, instead of whatever it is centered around (equivalent to removing the carrier wave from the signal). 
![[Pasted image 20240409181456.png]]
Signal centered at 0 Hz is #baseband, and signal based anywhere else is #bandpass. For a baseband, negative frequencies indicate frequencies lower than the carrier wave. If you see complex samples, you are in #baseband 
![[Pasted image 20240409181835.png]]
This is what is used in Direct Conversion. An alternative is Direct sampling, which retains the carrier frequency, but because of that it requires massive sample rate, therefore very expensive ADC

#### DC Spike 
Common in Direct conversion receivers. Sometimes if it is there, it may not really be there, for example when there is dc spike and everything else is noise. The DC spike is leakage from the Local Oscillator used in direct conv receiver.
![[Pasted image 20240409182757.png]]
Can be removed by **oversampling and off-tuning** . Bellow, green is the spectrum we want. To get that, we set SDR to pick up everything in the Blue sector. Since it is centered at 95 MHz, the DC spike will disappear when we later filter
![[Pasted image 20240409183507.png]]

#### Calculating power
Calculate average power by taking RMS of each sample in the signal
![[Pasted image 20240409184457.png]]
```Python
avg_pwr = np.mean(np.abs(x)**2)
```
If the mean of of all samples is around 0, can calculate by calculating the variance, because variance is equivalent to the equation above, plus a term for mean offset
```Python
avg_pwr = np.var(x) # (signal should have roughly zero mean)
```
This signal will be in the FREQUENCY DOMAIN 


### Modulation

#### Wireless symbols
![[Pasted image 20240409200450.png]]
Digital data is not transmitted directly, because:
- It has low freq components, namely DC 0Hz
- The sharp edges cause many spikes in over the spectrum
#### Differential coding
For BPSK, to determine if symbol is 180 deg outta phase, can use pilot symbols or differential coding