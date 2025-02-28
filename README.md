# <h1 align="center">Badr AI Receptionist</h1>

<p align="center">
  <img src="https://github.com/user-attachments/assets/3e7a0ad3-d860-4d55-9866-28d4739c3089" width="500"/>
</p>


> "From diagnosing patients to greeting visitors—Badr’s career change is proof that even robots can have a midlife crisis."


Badr is a repurposed medical simulation robot that has traded its stethoscope for a front desk. Once a high-tech medical training tool, Badr has now embraced a new mission—acting as an AI-powered receptionist that welcomes guests, manages schedules, and keeps things running smoothly.

## Overview

This public repository contains high-level documentation and architectural insights into the Badr AI Receptionist project. While the inner workings are fascinating, the actual implementation code is not included in this public repository.

Features

Motion Detection – Knows when someone arrives (no need to wave awkwardly).

Face Recognition – Identifies team members and frequent visitors (and remembers them better than most humans).

Voice Interaction – Supports both English and Arabic, including the Emirati dialect.

Natural Language Processing – Understands queries and generates useful responses (most of the time).

Appointment Scheduling – Handles meeting requests so humans don’t have to.

Email Notifications – Sends alerts for important events and system status updates.

Modular Architecture – Designed for easy customization and future expansions.


Minimum Hardware Requirements

Raspberry Pi 4B

Raspberry Pi Camera Module 3 Noir

USB PnP Audio Device (microphone and speaker)

PIR Sensor (for motion detection)


System Architecture

Directory Structure

/app – Core application code

/admin – Admin interface

/core – Core functionality

/face_recognition – Face recognition system

/hardware – Hardware interfaces

/integrations – External integrations

/nlp – Natural language processing

/speech – Speech processing


/config – Configuration files

/data – Data storage

/audio – Audio recordings

/faces – Face images and encodings

/images – Captured images

/logs – System logs

/videos – Recorded videos


/scripts – Utility scripts


## Key Components

State Machine – Manages conversation flow and system states.

PIR Sensor – Detects motion to activate the system.

Camera – Captures images and videos for face recognition.

Audio System – Handles speech input and output.

Face Recognizer – Identifies people from images.

NLP Engine – Processes text to understand intent and generate responses.

Email Service – Sends notifications and alerts.


## License

This project is licensed under a Proprietary License – see the LICENSE file for details.
Commercial use, reselling, or redistribution is strictly prohibited without explicit permission and royalty agreements.

## Contact

For inquiries, licensing, or partnerships, please reach out:
📧 Email: info.cognitara@gmail.com


---

Powered by Cognitara © 2025


