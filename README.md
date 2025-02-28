# Badr AI Receptionist

Badr is an Artificial Intelligent repurposed medical simulation robot to act as receptionist after retiring his medical journey.

An AI-driven virtual receptionist designed to automate front-desk interactions in a medical learning institute. The system handles incoming inquiries, schedules appointments, provides quick responses to FAQs, and integrates with existing business tools to streamline daily operations.

## Overview

This public repository contains high-level documentation and architecture information for the Badr AI Receptionist project. The actual implementation code is not included in this public repository.

## Features

- **Motion Detection**: Uses PIR sensor to detect presence and activate the system
- **Face Recognition**: Identifies team members and regular visitors
- **Voice Interaction**: Supports both English and Arabic (including Emirati dialect)
- **Natural Language Processing**: Understands intent and generates appropriate responses
- **Appointment Scheduling**: Manages meeting requests and notifies team members
- **Email Notifications**: Sends alerts for various events and system status
- **Modular Architecture**: Easy to extend and customize

## Hardware Requirements

- Raspberry Pi 4B
- Raspberry Pi module 3 noir camera
- USB PnP Audio Device (microphone and speaker)
- PIR Sensor (connected to GPIO 27)

## System Architecture

### Directory Structure

- `/app`: Core application code
  - `/admin`: Admin interface
  - `/core`: Core functionality
  - `/face_recognition`: Face recognition system
  - `/hardware`: Hardware interfaces
  - `/integrations`: External integrations
  - `/nlp`: Natural language processing
  - `/speech`: Speech processing
- `/config`: Configuration files
- `/data`: Data storage
  - `/audio`: Audio recordings
  - `/faces`: Face images and encodings
  - `/images`: Captured images
  - `/logs`: System logs
  - `/videos`: Recorded videos
- `/scripts`: Utility scripts

### Key Components

- **State Machine**: Manages conversation flow and system states
- **PIR Sensor**: Detects motion to activate the system
- **Camera**: Captures images and videos for face recognition
- **Audio System**: Handles speech input and output
- **Face Recognizer**: Identifies people from images
- **NLP Engine**: Processes text to understand intent and generate responses
- **Email Service**: Sends notifications and alerts

## License

This project is licensed under a Proprietary License - see the LICENSE file for details.
Commercial use, reselling, or redistribution is prohibited without explicit permission and royalty agreements.

## Contact

For more information or to inquire about licensing please contact:
- Email: badr.receptionist@gmail.com

---

Powered by Cognitara (c) 2025
