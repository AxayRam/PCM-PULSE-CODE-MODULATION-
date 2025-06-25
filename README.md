# PCM-PULSE-CODE-MODULATION-


🧠 What is PCM?

Pulse Code Modulation (PCM) is a method used to digitally represent analog signals. It samples the amplitude of the analog signal at uniform intervals and then quantizes the sample into a series of digital values. In this project, we simulate PCM using a sine wave.




---

📄 Project Title: Pulse Code Modulation (PCM) – Sine Wave Generation

This C program generates a sine wave audio signal (440 Hz, A4 note) and stores it in a .raw file format, simulating Pulse Code Modulation. The signal can be played back using tools like Audacity.


---

🔧 Requirements

A C compiler (e.g., GCC)

Audacity software

Math library (-lm flag)



---

🧾 Code Explanation

#include <stdio.h>
#include <math.h>
#define PI 3.14159265358979323846

int main() {
    float samples_per_second = 44100; // CD quality
    int duration_seconds = 2;         // Duration in seconds
    int max_value_encoding = 32767;   // Max for 16-bit signed PCM

    int i = 0;
    int total_samples = samples_per_second * duration_seconds;
    float time = 0;
    float angle;
    short int sample;

    FILE *file = fopen("sine.raw", "wb");
    if(file == NULL) {
        printf("could not open file for writing\n");
        return -1;
    }

    while(i < total_samples) {
        time = i * (1.0 / samples_per_second);
        angle = 2 * PI * 440 * time;
        sample = max_value_encoding * sin(angle);
        fwrite(&sample, 2, 1, file);
        printf("%d\n", sample);
        i++;
    }

    fclose(file);
    return 0;
}


---

🧪 How to Compile and Run

Use GCC with math library:

gcc sine_wave.c -o sine_wave -lm
./sine_wave


---

🔊 How to Open .raw File in Audacity

1. Open Audacity.


2. Go to File → Import → Raw Data.


3. Select sine.raw.


4. Use the following settings:

Encoding: Signed 16-bit PCM

Byte Order: Little-endian

Channels: 1 (Mono)

Sample Rate: 44100 Hz



5. Click "Import" to view/play your sine wave.




---

📌 Summary Table

Feature	Value

Frequency	440 Hz
Duration	2 seconds
Sample Rate	44100 Hz
Bit Depth	16-bit PCM
Output Format	.raw
Total Samples	88200



---

🧠 What is PCM?

Pulse Code Modulation (PCM) is a method to digitally represent analog signals. The amplitude of the analog signal is sampled at uniform intervals and each sample is quantized into a digital value.


