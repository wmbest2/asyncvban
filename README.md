# VBAN Protocol Wrapper

## Overview

This project aims to create a modern, ergonomic wrapper around the VBAN protocol. By leveraging modern Python tools such as dataclasses and asyncio, this wrapper provides a simple and efficient interface for working with VBAN.

## Features

- **Dataclasses**: Utilizes Python's dataclasses for clean, concise and ergonomic data structures.
- **Asyncio**: Supports asynchronous operations for non-blocking I/O.
- **Ease of Use**: Designed to be simple and intuitive, making it easy to integrate VBAN into your projects.

## Installation

To install the package, use pip:

```sh
pip install asyncvban
```

## Usage

### Basic Example

Here's a basic example of how to use the VBAN wrapper:

```python
from asyncvban import VBANAudioHeader, VBANPacket
from asyncvban.packet import VBANSampleRate

# Create a VBAN audio header
audio_header = VBANAudioHeader(sample_rate=VBANSampleRate.RATE_44100, channels=17, samples_per_frame=3,
                               bit_resolution=3, codec=0xf0, streamname="Channel1")

# Create a VBAN packet
packet = VBANPacket(header=audio_header)

# Access properties
print(packet.header.sample_rate)  # Output: 48000
print(packet.header.samples_per_frame)  # Output: 256
```

### Asynchronous Example

Using asyncio for non-blocking operations:

```python
import asyncio
from asyncvban.asyncio import AsyncVBANClient

# ... VBANAudioPlayer setup (see examples/audio_receiver.py)

client = AsyncVBANClient("bill.local", 6980, command_stream='Command1', audio_streams_in=['Windows Mic Out'])
receiver = VBANAudioPlayer(sample_rate=VBANSampleRate.RATE_44100, channels=2, client=client)

async def run_loop():
    await client.connect()
    await receiver.listen()

asyncio.run(run_loop())
```

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request with your changes.

## License

This project is licensed under the MIT License. See the `LICENSE` file for more details.

## Contact

For any questions or issues, please open an issue on the GitHub repository.

---

This README provides a brief overview of the project, installation instructions, usage examples, and contribution guidelines.