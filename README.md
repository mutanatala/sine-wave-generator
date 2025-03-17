# sine-wave-generator
import numpy as np
import simpleaudio as sa

def generate_sine_wave(frequency, duration, sample_rate=44100):
    """Generate a sine wave of a given frequency and duration."""
    t = np.linspace(0, duration, int(sample_rate * duration), False)
    wave = np.sin(2 * np.pi * frequency * t)
    wave = (wave * 32767).astype(np.int16)  # Convert to 16-bit PCM format
    return wave

def play_sine_wave(frequency, duration):
    """Play a sine wave sound."""
    wave_data = generate_sine_wave(frequency, duration)
    wave_obj = sa.WaveObject(wave_data, 1, 2, 44100)
    play_obj = wave_obj.play()
    play_obj.wait_done()

if __name__ == "__main__":
    print("🎵 Playing a 440Hz sine wave for 2 seconds...")
    play_sine_wave(440, 2)
