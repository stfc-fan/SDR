***
# Week 7 - Meeting 1 (18/3/24)

### Items/Questions Discussed
- How to take IQ stream and turn it into something to get frequency (SATNOGS DOES NOT CAPTURE IQ)
- Should I look at satellites that send continuously or just at particular points?
- Need a stable oscilator RTL dongle - will need to calibrate, need to know what the instantanious frequency of receiving of dongle is. GSM phone signals do a scan in frequency domanin, 
-  figuring out how to extract frequency infro from IQ file where u dont have a continuous signal, and how you turn it into a series of data points, run calibrations, lookup GPS phone network Calibrating RTL dongles.
- dongles sample at 8 bits, is that a problem?

### Actions for Meeting 2 
-  Need more detailed WBS
-  Look into IQ signals, how to work with them
- Look at notes by Brian
***
# Easter Meeting  (2/4/2024)
### Questions:
- [Richmond.pdf](file:///C:/Users/robya/Documents/123%20Space%20Engineering%20Materials/Project%20-%20Orbit%20Determination%20from%20Doppler%20Curves/Richmond.pdf) Talks about orbit determination of LEO, GEO and MEO sats, whereas the core ref [lu-et-al-2015-an-improved-orbit-determination-for-cubesats-using-doppler-shifts (1).pdf](file:///C:/Users/robya/Documents/123%20Space%20Engineering%20Materials/Project%20-%20Orbit%20Determination%20from%20Doppler%20Curves/lu-et-al-2015-an-improved-orbit-determination-for-cubesats-using-doppler-shifts%20(1).pdf) Only does so to re-estimate the Ballistic Coefficient B*, and uses that new estimate to correct for aerodynamic drag, which is main cause of position error in LEO. Which am I supposed to do? *The filter will give a more, not just balistic coeff*
- Do we need to carry out Simulations to test the B* correction algorithm, or just compare to measurements straight away? *will look at it later, could possibly do it*![[Pasted image 20240401170139.png]]
- Do we need spectrum analyzer for the frequency measurements or is that what the SDR is trying to replace? *signal processing done using python tools, and SDR will just give you the raw input*
- Is there a literature review that I need to carry out and report on before starting work
### TODO:
- Signal processing task to remove noise, Dr Yeomans will send a link
- How to turn the complex signal into something that numpy can work with
- Filtering, find carrier freq of signal, do a FFT fto find the carrier, but satelittes do not transmit the carrier. The carrier is not necessarily in the middle.. LEO sats do not broadcast the carrier. This is why u need to get rid of the noise. If its AWGN is ez to get rid off. 
- first do 3.1-3.4 before 2.5-2.8
- Week 10 and 11 need to make time for interim report in Gantt chart.
- Dont use funcube, its not that reliable anymore. use EVSQsat (bpsk) - in a good pass you can get 3000 frames.
- use python tools to visualise the data.
- Do a flowchart for interim report, to add in the signal processing, orbit generation block, the difference between the two is what goes into the batch estimator.
-