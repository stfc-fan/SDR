Based on [lu-et-al-2015-an-improved-orbit-determination-for-cubesats-using-doppler-shifts (1).pdf](file:///C:/Users/robya/Documents/123%20Space%20Engineering%20Materials/Project%20-%20Orbit%20Determination%20from%20Doppler%20Curves/lu-et-al-2015-an-improved-orbit-determination-for-cubesats-using-doppler-shifts%20(1).pdf)


Start with NORAD TLE as initial condition. Use Doppler signature to update the B* coefficient used in the SGP4 propagator

Doppler shift is related to **range rat**e via:
![[Pasted image 20240401115251.png]]
f0 - trans freq, fm - peak freq from SA.

Norad TLE+SGP4  gives coordinates in TEME, use DCM to convert to ECEF
To get **range rate** from SGP4+TLE, use:
![[Pasted image 20240401115910.png]]
The difference between both range rates gives the residual, which is where the update comes from.
![[Pasted image 20240401164829.png]]
After that, the A matrix is solved numerically 
![[Pasted image 20240401165555.png]]
From that, an improved estimate for B* ist taken by:
![[Pasted image 20240401165627.png]]


