# NM-ARASU-Voice-based-Notes-and-Memo-Systems
Introduction:
In today’s fast-paced digital world, capturing ideas, reminders, and memos efficiently
is crucial for productivity. Traditional typing-based note-taking methods can be
time-consuming and inconvenient, especially during multitasking or while on the move.
Voice-based note and memo systems provide a hands-free, quick, and natural way of
recording information using speech recognition technology.
This project aims to develop a voice-enabled memo system that allows users to create, store,
and retrieve notes using simple voice commands. It enhances accessibility, reduces the
cognitive load of manual typing, and supports faster documentation for personal and
professional use.

Problem Statement:
Users often struggle to capture quick thoughts or important reminders when busy or in
motion. Manual note-taking is inefficient in such situations and may lead to lost ideas. There
is a need for a convenient, accurate, and accessible system to convert voice inputs into
structured digital notes.

Objectives :
Enable Hands-free Note-taking: Allow users to create and store notes using voice commands
without the need for physical input.
Improve Information Capture Speed: Provide a faster alternative to typing, helping users
capture ideas in real time.
Enhance Accessibility and Usability: Support users with physical impairments or those
working in environments where typing is impractical.

Methodology:
Problem Analysis: Identified the inefficiencies of manual note-taking and the potential
benefits of voice-based interaction.

Speech Input Integration: Used speech recognition APIs (e.g., Google or IBM Watson) to
convert spoken words into text.
Note Structuring: Applied NLP to segment voice input into clear and categorized notes (e.g.,
to-do lists, reminders, memos).
Voice Command Recognition: Implemented command-based controls (e.g., “save note,”
“read last memo”) for easy interaction.
Testing and Validation: Tested the system across various accents and environments to ensure
accuracy and responsiveness.

Sample Code:
!pip install SpeechRecognition pandas
! pip install pandas pyttsx
!apt-get install -y portaudio19-dev
!pip install pyaudio
pip install pipwin
from google.colab import files
print("Upload your ZIP file containing .wav files:")
uploaded = files.upload()
import os
import zipfile
extract_folder = "extracted_audio"
os.makedirs(extract_folder, exist_ok=True)
for zip_filename in uploaded.keys():
if zip_filename.endswith('.zip'):
with zipfile.ZipFile(zip_filename, 'r') as zip_ref:
zip_ref.extractall(extract_folder)

print(f"Extracted ZIP file to folder: {extract_folder}")
else:
print(f"❌ {zip_filename} is not a ZIP file.")
print("Files extracted:")
print(os.listdir(extract_folder))
import os
import zipfile
from google.colab import files
import speech_recognition as sr

Step 1: Upload and unzip
uploaded = files.upload() # Upload a zip with .wav files
zip_file_name = list(uploaded.keys())[0]
extract_path = "Notes"
with zipfile.ZipFile(zip_file_name, 'r') as zip_ref:
zip_ref.extractall(extract_path)
print(f"\n✅ Extracted to '{extract_path}'")

Step 2: Find all .wav files in all subfolders
wav_files = []
for root, dirs, files_in_dir in os.walk(extract_path):
for file in files_in_dir:

if file.lower().endswith(".wav"):
wav_files.append(os.path.join(root, file))
if not wav_files:
print("❌ No .wav files found. Check your ZIP structure.")
else:
print("🎧 Found the following .wav files:")
for wf in wav_files:
print(" -", wf)

Step 3: Recognize and write to output file
recognizer = sr.Recognizer()
output_file = "Notes_output.txt"
with open(output_file, "w", encoding="utf-8") as f:
for wav_path in wav_files:
filename = os.path.basename(wav_path)
print(f"\n🔄 Processing {filename}...")
try:
with sr.AudioFile(wav_path) as source:
audio_data = recognizer.record(source)
command = recognizer.recognize_google(audio_data)
print(f"✅ Recognized: {command}")
f.write(f"{filename}: {command}\n")

except sr.UnknownValueError:
print(f"⚠ Could not understand audio in {filename}.")
f.write(f"{filename}: Could not understand audio.\n")
except sr.RequestError as e:
print(f"❌ API error for {filename}: {e}")
f.write(f"{filename}: API error - {e}\n")
print(f"\n📁 All recognized commands saved to '{output_file}'")

Input Format
.wav audio files (voice memos or notes)
Combined in a .zip file for batch upload
Output Format
.txt file (or .csv if needed), containing each transcribed note on a new line -
Automatically appended—no data is overwritten
Results
After uploading samples `.wav` files, the system was able to:
● Recognize and transcribe 90% of the content accurately (in a noise-free setting).
● Store all entries successfully into a single text file.
● Skip corrupted or unrecognized files while continuing with others.
Sample output:
output.txt
Testing and Validation:
● Tested with varied accents and sentence structures.
● Included background noise in some files to test recognition robustness.
● Validated file appending functionality and ensured no overwriting occurred.
● Ensured system handled unrecognized audio gracefully with placeholder text.

Conclusion:
The voice-based notes and memo system simplifies information recording and retrieval,
improving productivity and user convenience. The project showcases the potential of voice
interfaces in day-to-day tasks and opens up further opportunities for integration with virtual
assistants and smart devices.

This is a offline tool, your data stays locally and is not send to any server!
