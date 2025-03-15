# Architecture

## Overview

This project creates a Raspberry Pi-based audio server that:
1. Receives audio via AirPlay using Shairport Sync
2. Processes and distributes the audio using Snapcast Server
3. Provides a web interface (Snapweb) for controlling playback and devices

## Audio Pipeline

![architecture](/assets/architecture.png)

## System Components

### Hardware
- **Raspberry Pi**: Central processing unit running all server components
- **Audio Output Device**: DAC (Digital-to-Analog Converter) or audio HAT for quality audio output
- **Network Interface**: Ethernet or WiFi for connectivity

### Software

#### Core Services
- **Shairport Sync**: Open-source AirPlay audio receiver that emulates an AirPlay endpoint
- **Snapcast Server**: Audio streaming server that distributes synchronized audio
- **Snapcast Client**: Audio playback client that receives streams from Snapcast Server
- **Snapweb**: Web interface for controlling Snapcast system

## Component Details

### Shairport Sync
- Emulates an AirPlay receiver
- Accepts audio streams from iOS devices, macOS, etc.
- Decodes the audio and passes it to the system's audio pipeline
- Can provide metadata about current playback

### Snapcast
- **Server Component**:
  - Receives audio from Shairport Sync
  - Distributes synchronized audio streams to clients
  - Manages client connections and synchronization
  
- **Client Component**:
  - Receives audio from Snapcast Server
  - Plays back audio in perfect sync with other clients
  - Can be run on the same Raspberry Pi or on separate devices

### Snapweb
- Web interface for Snapcast
- Provides controls for:
  - Volume adjustment
  - Client management
  - Group management
  - Stream selection

## Network Configuration

- **Port Requirements**:
  - AirPlay: TCP ports 5000-5005, 7000, UDP port 6000-6010
  - Snapcast Server: TCP port 1704-1705
  - Snapweb interface: TCP port 1780

## Audio Quality Considerations

- Sample Rate: 44.1kHz (AirPlay standard)
- Bit Depth: 16-bit or 24-bit depending on configuration
- Format: PCM or compressed depending on network conditions

## Security Considerations

- AirPlay traffic can be encrypted
- Local network isolation recommended
- Firewall configuration to restrict access to necessary services only

## Scaling

The architecture can be expanded to support:
- Multiple audio zones with synchronized playback
- Additional input sources beyond AirPlay
- Integration with home automation systems 