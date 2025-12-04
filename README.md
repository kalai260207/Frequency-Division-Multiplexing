# Frequency-Division-Multiplexing


Aim:

To study and implement Frequency Division Multiplexing (FDM) and Demultiplexing using SCILAB by combining six different message signals into a single composite signal for transmission and then recovering each message signal at the receiver through demodulation and filtering.
Apparatus Required:
Computer system with SCILAB software installed.

Theory:

Frequency Division Multiplexing (FDM) is a technique in which multiple message signals are transmitted simultaneously over a single communication channel by assigning each signal a unique carrier frequency. Each message is modulated with its respective carrier so that their frequency bands do not overlap. These modulated signals are then combined to form a single multiplexed signal for transmission. At the receiver end, the signal is demultiplexed by using the same carrier frequencies for demodulation, followed by low-pass filtering to recover the original baseband signals. FDM is widely used in radio broadcasting, cable television, and satellite communication systems where efficient bandwidth utilization is essential.

Algorithm:

1.Start the program and initialize the sampling frequency fs and time vector t.
2.Generate six message signals of different frequencies (150 Hz to 900 Hz) using sine functions.

3.Assign six distinct carrier frequencies (3 kHz to 13 kHz) to each message signal to avoid overlap.

4.Modulate each message signal by multiplying it with its corresponding carrier (Amplitude Modulation).

5.Add all modulated signals to obtain the combined FDM signal representing multiple channels.

6.Plot all six message signals and the multiplexed signal for observation.



7.Demodulate each signal by multiplying the FDM signal with its corresponding carrier frequency.

8.Apply a low-pass filter to extract the original baseband signals (recovering the messages).

9.Plot the demodulated signals to verify successful recovery.

10.End the program after confirming proper multiplexing and demultiplexing operation.

CODE:

Fs = 65000;                
t = 0:1/Fs:0.02;
m1 = 1.6 * sin(2*%pi*300*t);
m2 = 1.4 * sin(2*%pi*400*t);
m3 = 1.8 * sin(2*%pi*500*t);
m4 = 2.0 * sin(2*%pi*600*t);
m5 = 2.2 * sin(2*%pi*700*t);
m6 = 2.4 * sin(2*%pi*800*t);

c1 = 6000;
c2 = 10000;
c3 = 14000;
c4 = 18000;
c5 = 22000;
c6 = 26000;


carrier1 = cos(2*%pi*c1*t);
carrier2 = cos(2*%pi*c2*t);
carrier3 = cos(2*%pi*c3*t);
carrier4 = cos(2*%pi*c4*t);
carrier5 = cos(2*%pi*c5*t);
carrier6 = cos(2*%pi*c6*t);


s1 = m1 .* carrier1;
s2 = m2 .* carrier2;
s3 = m3 .* carrier3;
s4 = m4 .* carrier4;
s5 = m5 .* carrier5;
s6 = m6 .* carrier6;

s_total = s1 + s2 + s3 + s4 + s5 + s6;


r2 = s_total .* carrier2;
r3 = s_total .* carrier3;
r4 = s_total .* carrier4;
r5 = s_total .* carrier5;
r6 = s_total .* carrier6;

function y = ideal_lowpass_fft(x, Fs, fc)
    N = length(x);
    X = fft(x);
    f = Fs*(0:N-1)/N;
    mask = (f <= fc) | (f >= Fs-fc);
    Y = X .* mask;
    y = real(ifft(Y));
endfunction

fc = 1500; // Changed but still above message frequencies

// Recovered signals
dm1 = ideal_lowpass_fft(r1, Fs, fc);
dm2 = ideal_lowpass_fft(r2, Fs, fc);
dm3 = ideal_lowpass_fft(r3, Fs, fc);
dm4 = ideal_lowpass_fft(r4, Fs, fc);
dm5 = ideal_lowpass_fft(r5, Fs, fc);
dm6 = ideal_lowpass_fft(r6, Fs, fc);

// Plots
figure(1);
subplot(3,2,1); plot(t,m1); title("Message Signal 1");
subplot(3,2,2); plot(t,m2); title("Message Signal 2");
subplot(3,2,3); plot(t,m3); title("Message Signal 3");
subplot(3,2,4); plot(t,m4); title("Message Signal 4");
subplot(3,2,5); plot(t,m5); title("Message Signal 5");
subplot(3,2,6); plot(t,m6); title("Message Signal 6");

figure(2);
plot(t, s_total); title("Multiplexed FDM Signal");

figure(3);
subplot(3,2,1); plot(t,dm1); title("Recovered Signal 1");
subplot(3,2,2); plot(t,dm2); title("Recovered Signal 2");
subplot(3,2,3); plot(t,dm3); title("Recovered Signal 3");
subplot(3,2,4); plot(t,dm4); title("Recovered Signal 4");
subplot(3,2,5); plot(t,dm5); title("Recovered Signal 5");
subplot(3,2,6); plot(t,dm6); title("Recovered Signal 6");

Output Waveform

![WhatsApp Image 2025-11-30 at 3 03 41 PM](https://github.com/user-attachments/assets/eda582a6-b171-4f9b-92f6-2ec2910286d3)

![WhatsApp Image 2025-11-30 at 3 04 24 PM](https://github.com/user-attachments/assets/c04551be-c3d1-43a6-b24a-0e1bc548ed23)

![WhatsApp Image 2025-11-30 at 3 04 55 PM](https://github.com/user-attachments/assets/75300b25-3d13-429e-9db6-f312d6e5b157)

TABULATION:
![WhatsApp Image 2025-12-04 at 3 43 49 PM](https://github.com/user-attachments/assets/93a0b1f4-de24-4fa5-9f99-77d41a830d05)

![WhatsApp Image 2025-12-04 at 3 44 03 PM](https://github.com/user-attachments/assets/a936f8d9-ff97-48ee-ad34-9690f86b1445)


Result:

The Frequency Division Multiplexing (FDM) and Demultiplexing of six different message signals were successfully implemented using SCILAB.All six message signals were modulated with distinct carrier frequencies and combined to form a single multiplexed signal. Upon demodulation and low-pass filtering, each original message signal was accurately recovered, verifying the correct working of the FDM and demultiplexing process.
