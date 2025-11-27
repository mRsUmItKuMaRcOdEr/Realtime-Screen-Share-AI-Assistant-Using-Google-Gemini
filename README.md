Realtime Screen-Share AI Assistant Using Google Gemini

This project is a real-time multimodal AI assistant capable of analyzing screen-sharing video input and live audio to generate text and audio responses using Google Gemini. It integrates a modern web interface with a Python WebSocket backend, enabling simultaneous video frame processing, audio streaming, and real-time AI output.

Features
Real-Time Screen Sharing

The frontend captures the user’s screen and extracts frames periodically for analysis. The screen capture is handled using JavaScript APIs and sent to the backend as Base64-encoded JPEG frames.
(Frontend reference: index.html) 

index

Live Audio Streaming

The application records microphone input using AudioContext, ScriptProcessorNode, and a custom AudioWorklet processor (pcm-processor.js). The audio stream is captured as 16-bit PCM and transmitted to the backend for real-time processing.
(Audio processor reference: pcm-processor.js) 

pcm-processor

WebSocket Communication

A persistent WebSocket connection transfers audio and video chunks from the client to the server. The backend streams these inputs to Google Gemini and returns generated text and synthesized audio chunks to the client.

Gemini Integration

The backend uses Google’s multimodal Gemini API for live audio and vision inference. The assistant responds with text during the conversation and generates audio that is streamed back to the frontend.
(Backend reference: main.py) 

main

Real-Time Chat Display

All text responses from Gemini are displayed in a scrollable chat interface styled through Material Design Lite. The frontend also plays AI-generated audio streams as they are received.

Project Structure
project/
│── index.html          # Frontend interface for screen sharing and audio input
│── main.py             # Python WebSocket server connected to Google Gemini
│── pcm-processor.js    # AudioWorklet processor for PCM streaming
│── readme              # Original readme file

How It Works

The frontend captures screen frames using getDisplayMedia, draws them on a hidden canvas, and extracts JPEG Base64 strings.

The microphone input is recorded as raw PCM audio using a ScriptProcessorNode and processed using an AudioWorklet.

Both audio and image chunks are sent to the backend through a WebSocket connection.

The backend forwards these chunks to Gemini via the live API session.

Gemini returns text responses and generated audio segments, which are streamed back to the client in real time.

The frontend updates the chat log and plays audio responses synchronized with the interaction.

Installation and Setup
Requirements

Python 3.10+

Node-enabled browser (Chrome recommended)

Google Gemini API key

Python Dependencies

Install the required packages:

pip install websockets google-generativeai google-genai pydub

Running the Backend

Start the WebSocket server:

python main.py


This starts the backend on:

ws://localhost:9083

Running the Frontend

Open index.html directly in a browser or serve it through a local server.

The application will automatically:

Start screen sharing

Initialize microphone input

Connect to the backend WebSocket

Key Components
Frontend (index.html)

Handles UI, screen capture, audio recording, WebSocket sending, and chat display.
Includes styling and Material Design Lite layout.


index

Backend (main.py)

Implements:

WebSocket server

Gemini live session

Audio and image forwarding

Response handling

PCM-to-MP3 transcription pipeline


main

Audio Processing (pcm-processor.js)

Implements a custom AudioWorklet processor for buffered PCM playback.


pcm-processor

Technical Highlights

Real-time multimodal streaming pipeline

Custom PCM buffer handling using AudioWorklet

Live Gemini vision and audio integration

Automated speech transcription using Gemini Flash 1.5

Clean WebSocket communication loop (send + receive tasks)

Modern UI with Material Design Lite styling

Encoded media chunks for low-latency streaming

Future Improvements

Add user controls for frame capture frequency

Provide UI for selecting different screen regions

Add option to save chat transcripts

Implement authentication and secure WebSocket handling

Expand to browser-based deployment with HTTPS
