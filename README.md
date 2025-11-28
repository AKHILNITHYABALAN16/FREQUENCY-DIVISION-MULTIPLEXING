# FREQUENCY-DIVISION-MULTIPLEXING
AIM

To implement Frequency Division Multiplexing (FDM) for six different message signals using Scilab, generate the multiplexed signal, and perform demultiplexing to recover all the original message signals. The experiment also includes plotting the message signals, multiplexed signal, and demultiplexed signals.

APPARATUS REQUIRED
Computer System

Scilab Software

ALGORITHM

Set sampling frequency, time duration, and time vector.

Generate six message signals with different frequencies.

Assign six different carrier frequencies.

Perform DSB-SC modulation by multiplying each message with its carrier.

Add all modulated signals to form the multiplexed FDM signal.

For each channel, multiply the multiplexed signal with the same carrier (demodulation).

Apply a low-pass filter to extract the recovered message.

Plot message signals, multiplexed signal, and recovered s ignals.

THEORY

Frequency Division Multiplexing (FDM) is a technique in which multiple message signals are transmitted simultaneously over a single communication channel by assigning each signal a different carrier frequency. Each message modulates its own carrier, and all modulated signals are added to form the multiplexed signal. Since the carrier frequencies are well separated, the signals do not overlap in the frequency domain.

At the receiver, each signal is recovered by multiplying the multiplexed signal with the corresponding carrier (coherent demodulation) and passing it through a low-pass filter to extract the original baseband message. FDM is widely used in radio broadcasting, telephone systems, and cable TV.

PROGRAM
~~~~
clc; 
clear; 
close;

fs = 50000;
t = 0:1/fs:0.05;

m1 = 1.7*sin(2*%pi*163*t);
m2 = 1.8*sin(2*%pi*173*t);
m3 = 1.9*sin(2*%pi*183*t);
m4 = 2.0*sin(2*%pi*193*t);
m5 = 2.1*sin(2*%pi*203*t);
m6 = 2.2*sin(2*%pi*213*t);

c1 = cos(2*%pi*2000*t);
c2 = cos(2*%pi*4000*t);
c3 = cos(2*%pi*6000*t);
c4 = cos(2*%pi*8000*t);
c5 = cos(2*%pi*10000*t);
c6 = cos(2*%pi*12000*t);

s1 = m1 .* c1;
s2 = m2 .* c2;
s3 = m3 .* c3;
s4 = m4 .* c4;
s5 = m5 .* c5;
s6 = m6 .* c6;

fdm = s1 + s2 + s3 + s4 + s5 + s6;

r1 = fdm .* c1;
r2 = fdm .* c2;
r3 = fdm .* c3;
r4 = fdm .* c4;
r5 = fdm .* c5;
r6 = fdm .* c6;


cutoff_hz = 400;
norm_cutoff = cutoff_hz/(fs/2);

M = 101; 

[h, w] = wfir('lp', M, [norm_cutoff, 0], 'hm', 0);  

d1 = conv(r1, h, 'same');
d2 = conv(r2, h, 'same');
d3 = conv(r3, h, 'same');
d4 = conv(r4, h, 'same');
d5 = conv(r5, h, 'same');
d6 = conv(r6, h, 'same');

d1 = 2 * d1;
d2 = 2 * d2;
d3 = 2 * d3;
d4 = 2 * d4;
d5 = 2 * d5;
d6 = 2 * d6;

figure(1);
subplot(3,2,1); plot(t,m1); title("Message 1");
subplot(3,2,2); plot(t,m2); title("Message 2");
subplot(3,2,3); plot(t,m3); title("Message 3");
subplot(3,2,4); plot(t,m4); title("Message 4");
subplot(3,2,5); plot(t,m5); title("Message 5");
subplot(3,2,6); plot(t,m6); title("Message 6");

figure(2);
plot(t,fdm); title("Multiplexed FDM");

figure(3);
subplot(3,2,1); plot(t,d1); title("Demod 1");
subplot(3,2,2); plot(t,d2); title("Demod 2");
subplot(3,2,3); plot(t,d3); title("Demod 3");
subplot(3,2,4); plot(t,d4); title("Demod 4");
subplot(3,2,5); plot(t,d5); title("Demod 5");
subplot(3,2,6); plot(t,d6); title("Demod 6");
~~~~~
OUTPUT WAVEFORM

<img width="1920" height="1200" alt="Screenshot (128)" src="https://github.com/user-attachments/assets/9bf00d41-ff4b-4e30-a2c0-6a8ed871160c" />
<img width="1920" height="1200" alt="Screenshot (130)" src="https://github.com/user-attachments/assets/94c51e89-5214-47aa-940e-cc270af49ef9" />
<img width="1920" height="1200" alt="Screenshot (129)" src="https://github.com/user-attachments/assets/59a6d872-3882-4ed9-acaf-604140b73b91" />

CALCULATION

RESULT

Six different message signals were generated and modulated using FDM. All modulated signals were added to form a multiplexed FDM signal. Each message was successfully recovered using coherent demodulation followed by low-pass filtering. The plots confirmed accurate multiplexing and demultiplexing.

