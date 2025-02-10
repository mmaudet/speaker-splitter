# Speaker Splitter

A Python tool to separate audio files by speaker using diarization data. This tool takes a WAV audio file and a JSON file containing speaker timestamps, and creates individual WAV files for each speaker, maintaining the original timing and replacing other speakers' segments with silence.

![Speaker Splitter](/assets/images/Speaker-Splitter-workflow.png)

## Features

- Separates multi-speaker audio into individual speaker files
- Preserves original timing and audio quality
- Handles timestamps in HH:MM:SS,MMM format
- Creates silence during non-speaking segments
- Supports multiple speakers
- Simple command-line interface

## Prerequisites

- Python 3.11 or higher
- `pydub` library for audio processing
- FFmpeg (required by pydub)

## Installation

1. Clone the repository:
```bash
git clone https://github.com/mmaudet/speaker-splitter.git
cd speaker-splitter
```

2. Create and activate a Conda environment:
```bash
conda create -n audio-splitter python=3.11
conda activate audio-splitter
```

3. Install required Python packages:
```bash
pip install pydub
```

4. Install FFmpeg:
- Ubuntu/Debian:
  ```bash
  sudo apt-get install ffmpeg
  ```
- macOS:
  ```bash
  brew install ffmpeg
  ```

## Usage

The basic command format is:
```bash
python speaker_splitter.py input.wav diarization.json
```

### Input Files

1. Audio file (`input.wav`):
   - Must be in WAV format
   - Contains the multi-speaker audio to be separated

2. JSON file (`diarization.json`):
   - Contains speaker segments with timestamps
   - Can be generated using various diarization tools such as:
     - [WhisperX](https://github.com/m-bain/whisperX): an open-source tool that combines Whisper with speaker diarization
     - [LinTO](https://linto.app): an enterprise-grade conversational AI platform developed by [LINAGORA](https://www.linagora.com)
   - Format example:
```json
{
  "segments": [
    {
      "speaker": "SPEAKER_00",
      "start": "00:01:57,000",
      "end": "00:01:59,000",
      "text": "Example text"
    },
    {
      "speaker": "SPEAKER_01",
      "start": "00:02:14,000",
      "end": "00:02:20,000",
      "text": "Another example"
    }
  ]
}
```

#### Generating the JSON File

1. Using WhisperX:
```bash
# Install WhisperX
pip install whisperx

# Run diarization
whisperx audio.wav --diarize
```

2. Using LinTO:
   - Visit [LinTO Platform](https://linto.app)
   - Upload your audio file
   - Use the transcription and diarization service
   - Export the results in JSON format

Both tools provide accurate speaker diarization and transcription, with the JSON output being compatible with this tool.

### Output

The script generates separate WAV files for each speaker:
- `output-audio-SPEAKER_00.wav`
- `output-audio-SPEAKER_01.wav`
- etc.

Each output file:
- Has the same duration as the input file
- Contains only the specified speaker's segments
- Contains silence during other speakers' segments
- Maintains original timing and audio quality

## Error Handling

The script includes error handling for common issues:
- Invalid input files
- Incorrect JSON format
- Missing audio file
- Invalid timestamps
- Python version verification

## Future Developments (not planned yet)
- WhisperX Integration: a major planned enhancement is the direct integration of WhisperX for a complete transcription and diarization workflow
- Audio Format Support: add support for additional audio formats such as MP3, FLAC, etc.
- Cross-fade between segments to reduce abrupt transitions
- Simple web interface for file upload and processing and real-time processing status
- Speech overlap detection and handling
- Process multiple files in batch
- Docker container for easy deployment
- Integration with LinTO platform

## Contributing

Contributions are welcome! Please feel free to submit pull requests.
- Submit pull requests for any of these features
- Propose new features or improvements
- Report bugs or issues
- Share use cases and requirements

## License

This project is licensed under the GNU Affero General Public License v3.0 (AGPL-3.0). This license ensures that:
- You can use, modify, and distribute the software
- If you modify the software and provide it as a service over a network, you must make the source code available
- Any derivative work must also be licensed under AGPL-3.0

See the [LICENSE](https://www.gnu.org/licenses/agpl-3.0.en.html) for the full text of the license.

## Acknowledgments

- Uses `pydub` for audio processing
- Inspired by the need for clean speaker separation in multi-speaker recordings
- Thanks to the WhisperX and LinTO teams for providing excellent diarization tools
