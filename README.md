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

fs = 25000;              
t = 0:1/fs:0.04;        

fm = [80, 160, 240, 320, 400, 480]; 
m = [];

for i = 1:6
    m(i, :) = sin(2*%pi*fm(i)*t);
end

fc = [2500, 3500, 4500, 5500, 6500, 7500];

fdm = zeros(1, length(t));
for i = 1:6
    c = cos(2*%pi*fc(i)*t);
    s = m(i, :) .* c;
    fdm = fdm + s;
end

scf(1);
clf;
for i = 1:6
    subplot(6,1,i);
    plot(t, m(i, :));
end

scf(2);
clf;
plot(t, fdm);

demod = [];
for i = 1:6
    c = cos(2*%pi*fc(i)*t);
    x = fdm .* c;
    h = ones(1,100)/100;
    y = conv(x, h, 'same');
    demod(i, :) = y;
end

scf(3);
clf;
for i = 1:6
    subplot(6,1,i);
    plot(t, demod(i, :));
end

disp("FDM and Demultiplexing completed with NEW frequencies!");

~~~~~
OUTPUT WAVEFORM

<img width="1920" height="1200" alt="Screenshot (133)" src="https://github.com/user-attachments/assets/235ebd6b-b1bf-4075-8cb4-1b1d32484e1a" />

<img width="1920" height="1200" alt="Screenshot (134)" src="https://github.com/user-attachments/assets/3a61174e-5517-43c6-8e61-7e3e9d93bb89" />

<img width="1920" height="1200" alt="Screenshot (135)" src="https://github.com/user-attachments/assets/ad3fb743-f2d8-4f65-a3c3-5878aca0ece4" />


CALCULATION

![WhatsApp Image 2025-11-29 at 14 14 59_5b0a1174](https://github.com/user-attachments/assets/cdcda932-4ee1-48c0-89e1-0f600dd2dcc0)

![WhatsApp Image 2025-11-29 at 14 14 59_ea1ca2fe](https://github.com/user-attachments/assets/5f976da1-d7c4-4ce6-8288-dd35279fcdc6)



RESULT

Six different message signals were generated and modulated using FDM. All modulated signals were added to form a multiplexed FDM signal. Each message was successfully recovered using coherent demodulation followed by low-pass filtering. The plots confirmed accurate multiplexing and demultiplexing.

