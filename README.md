# Enhanced Multi-Client File Transfer System

A robust Python-based file transfer system that supports multiple concurrent clients with features like encryption, compression, bandwidth control, and automatic retransmission.

## Features

- **Multi-Client Support**: Handle multiple concurrent file transfers
- **Secure Transfer**: End-to-end encryption using Fernet encryption
- **Data Compression**: Automatic compression using zlib
- **Bandwidth Control**: Configurable bandwidth limiting
- **Progress Tracking**: Real-time transfer progress and speed monitoring
- **Error Recovery**: Automatic retransmission of failed chunks
- **Connection Management**: Timeout handling and connection monitoring
- **Checksums**: File integrity verification using SHA256

## Requirements

- Python 3.7+
- Required packages:
  ```
  cryptography
  aiometer
  ```

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/maximuscle/BigEndian-Challenge.git
   cd enhanced-file-transfer
   ```

2. Install dependencies:
   ```bash
   pip install cryptography aiometer
   ```

## Usage

### Basic Usage

1. Start the server:
```python
from enhanced_file_transfer import EnhancedFileTransferServer

async def main():
    server = EnhancedFileTransferServer(password="your_secret_password")
    await server.start()

if __name__ == "__main__":
    import asyncio
    asyncio.run(main())
```

2. Create a client and transfer files:
```python
from enhanced_file_transfer import EnhancedFileTransferClient

async def main():
    client = EnhancedFileTransferClient(
        "client_1",
        password="your_secret_password"
    )
    success = await client.transfer_file("path/to/your/file.txt")
    print(f"Transfer {'successful' if success else 'failed'}")

if __name__ == "__main__":
    import asyncio
    asyncio.run(main())
```

### Advanced Configuration

You can customize various parameters:

```python
# Server configuration
server = EnhancedFileTransferServer(
    host='localhost',
    port=8888,
    password="your_secret_password"
)

# Client configuration
client = EnhancedFileTransferClient(
    client_id="custom_client",
    host='localhost',
    port=8888,
    password="your_secret_password"
)
```

## Architecture

The system consists of several key components:

1. **EnhancedFileTransferServer**: Handles multiple client connections and file transfers
2. **EnhancedFileTransferClient**: Manages file uploads and downloads
3. **RetransmissionQueue**: Handles failed chunk retransmission
4. **BandwidthLimiter**: Controls transfer speeds
5. **ProgressTracker**: Monitors transfer progress
6. **Encryption**: Manages secure data transfer
7. **Compression**: Handles data compression

## Configuration

Key constants that can be modified in `enhanced_file_transfer.py`:

```python
CHUNK_SIZE = 1024  # Size of each file chunk in bytes
MAX_RETRIES = 3    # Maximum number of retransmission attempts
CONNECTION_TIMEOUT = 30  # Connection timeout in seconds
BANDWIDTH_LIMIT = 1024 * 1024  # 1 MB/s bandwidth limit
COMPRESSION_LEVEL = 6  # Zlib compression level (0-9)
```

## Error Handling

The system includes comprehensive error handling:

- Connection timeouts
- Corrupted packets
- Missing chunks
- Network errors
- Encryption/decryption failures

## Performance Considerations

- **Memory Usage**: Large files are processed in chunks to minimize memory usage
- **CPU Usage**: Compression level can be adjusted to balance CPU usage vs. transfer speed
- **Network**: Bandwidth limiting prevents network saturation
- **Concurrency**: Async implementation allows efficient handling of multiple clients


## Acknowledgments

- Built using Python's asyncio for asynchronous I/O
- Encryption provided by the cryptography package
- Compression using zlib

