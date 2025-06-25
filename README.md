# PCM-PULSE-CODE-MODULATION-


🧠 What is PCM?

Pulse Code Modulation (PCM) is a method used to digitally represent analog signals. It samples the amplitude of the analog signal at uniform intervals and then quantizes the sample into a series of digital values. In this project, we simulate PCM using a sine wave.


📁 Project Title: Pulse Code Modulation (PCM) – Sine Wave Generation

This C program generates a sine wave audio signal (440 Hz, A4 note) and stores it in a .raw file format, simulating Pulse Code Modulation. This signal can be played back or viewed using audio tools like Audacity 🎧.


🔧 Requirements

A C compiler (e.g., GCC)
Audacity (or any other RAW audio player/viewer)
Math library (-lm flag required)


🧾 Description of Code

#include <stdio.h>
#include <math.h>
#define PI 3.14159265358979323846
stdio.h: Used for file operations.
math.h: Required for the sin() function to compute the sine wave.
PI: A constant used in sine wave formula.
int main() {
    float samples_per_second = 44100; // 📦 Standard CD quality (44.1kHz)
    int duration_seconds = 2;         // 🕒 Duration of audio in seconds
    int max_value_encoding = 32767;   // 🎚 Max value for 16-bit signed PCM audio
Sampling Rate = 44,100 samples/sec (CD quality)
Duration = 2 seconds
Max amplitude = 32767 (16-bit signed integer range)

int i = 0;
    int total_samples = samples_per_second * duration_seconds;
    float time = 0;
    float angle;
    short int sample;
total_samples = Total number of samples to generate
time & angle: Used to calculate the sine wave
sample: Stores each 16-bit PCM value

FILE *file;
    file = fopen("sine.raw", "wb");
    if(file == NULL) {
        printf("could not open file for writing\n");
        return -1;
    }
Opens a binary file sine.raw to store PCM data
If file can't be created, shows error and exits

while(i < total_samples) {
        time = i * (1.0 / samples_per_second);  // 🕓 Convert sample number to time
        angle = 2 * PI * 440 * time;            // 🔊 440 Hz frequency = A4 musical note
        sample = max_value_encoding * sin(angle); // 📈 Compute sine wave amplitude
        fwrite(&sample, 2, 1, file);            // 💾 Write 16-bit sample to file
        printf("%d\n", sample);                 // 🖨 Print value for debug
        i++;
    }
Loop generates all samples for 2 seconds
440 Hz is used as the sine wave frequency
Each sample is calculated using sine function
Written in little-endian 16-bit PCM format

fclose(file); // ✅ Close the file
return 0;     // ✅ Successful program end
}

🧪 How to Compile and Run
Make sure to compile using the -lm flag to link the math library:
gcc sine_wave.c -o sine_wave -lm
Then run:
./sine_wave


🔊 How to Open .raw File in Audacity
1. Open Audacity.
2. Go to File → Import → Raw Data.
3. Select the file sine.raw.
4. Use the following settings:
Encoding: Signed 16-bit PCM
Byte order: Little-endian
Channels: 1 (Mono)
Sample rate: 44100 Hz
5. Click Import.



You will now see and hear your sine wave 🎶.
