# Neo Systema Audio Analyzer

A comprehensive audio analysis tool that combines multiple analysis methods into a unified system:

- 🎵 **Audio Feature Extraction** - Energy, spectral features, rhythm analysis
- 🎹 **MIDI Note Data** - Import precise timing from MIDI files  
- 📝 **Lyric Alignment** - Word-level timing using Montreal Forced Aligner
- 🖥️ **Dual Interface** - Command-line and GUI versions available

## Features

### Core Audio Analysis
- **Energy Analysis**: Total, harmonic, and percussive components
- **Spectral Features**: Centroid, contrast, rolloff
- **MFCCs**: 13-coefficient timbral analysis
- **Rhythm Detection**: Beat positions and onset detection
- **Configurable Frame Rate**: Adjustable analysis resolution

### MIDI Integration
- Extract all notes with precise timing
- Velocity (loudness) information
- Track and channel preservation
- Tempo change handling

### Lyric Alignment
- **Automatic Alignment**: Using Montreal Forced Aligner (MFA)
- **Manual Timing**: Interactive pygame interface as fallback
- **Plain Text Storage**: For lyrics without timing

## Quick Start

### 1. Installation

```bash
# Create conda environment
conda create -n neo_systema python=3.10
conda activate neo_systema

# Install Python dependencies
pip install librosa numpy scipy pyyaml tqdm soundfile

# Optional: MIDI support
pip install mido

# Optional: Manual timing interface
pip install pygame

# Optional: MFA for automatic lyric alignment
conda install -c conda-forge montreal-forced-aligner
mfa model download acoustic english_us_arpa
mfa model download dictionary english_us_arpa
```

### 2. Usage Options

#### GUI Version (Recommended)
```bash
python neo_systema_gui.py
```

#### Command Line Version
```bash
# Interactive mode
python neo_systema_analyzer_clean.py

# Direct file specification
python neo_systema_analyzer_clean.py /path/to/audio.wav
```

### 3. Basic Configuration

Create a `config.yaml` file (optional):

```yaml
# Analysis settings
analysis_fps: 20
output_dir: "./data"

# MFA settings (if available)
mfa_output_dir: "./mfa_output"
mfa:
  mfa_executable_path: "/path/to/mfa"  # Use 'which mfa' to find
  dictionary: "english_us_arpa"
  acoustic_model: "english_us_arpa"
```

## Interface Options

### GUI Interface
- **File Selection**: Browse for audio/MIDI files
- **Settings Panel**: Configure analysis parameters
- **Progress Tracking**: Real-time analysis updates
- **Results Display**: Comprehensive analysis summary
- **Settings Management**: Save/load configurations

### Command Line Interface  
- **Flexible Input**: Prompt for audio file or use argument
- **Interactive Prompts**: Optional MIDI and lyrics inclusion
- **Progress Bars**: Visual progress indication
- **Comprehensive Output**: Detailed JSON results

## Output Format

The analyzer generates a comprehensive JSON file with the following structure:

```json
{
  "metadata": {
    "source_file": "song.wav",
    "duration_seconds": 180.5,
    "sample_rate": 44100,
    "analysis_fps": 20,
    "global_tempo_bpm": 120.0
  },
  "structure": {
    "beats": [0.5, 1.0, 1.5, ...],
    "onsets": [0.0, 0.5, 1.0, ...]
  },
  "features_per_frame": [
    {
      "timestamp": 0.0,
      "energy": {
        "rms_total": 0.05,
        "rms_harmonic": 0.03,
        "rms_percussive": 0.02
      },
      "spectral": {
        "centroid": 1500.0,
        "contrast_mean": 25.0,
        "rolloff": 2000.0
      },
      "mfcc_vector": [1.2, -0.5, ...]
    }
  ],
  "musical_notes": {
    "source": "MIDI",
    "note_count": 245,
    "notes": [
      {
        "pitch": 60,
        "pitch_name": "C4",
        "velocity": 100,
        "start_time": 0.5,
        "duration": 0.25
      }
    ]
  },
  "lyrics": {
    "source": "MFA",
    "timed": true,
    "word_count": 42,
    "timed_words": [
      {
        "word": "Hello",
        "start_time": 0.5,
        "end_time": 0.8
      }
    ]
  }
}
```

## Advanced Usage

### MFA Setup for Lyric Alignment

```bash
# Install MFA
conda install -c conda-forge montreal-forced-aligner

# Download models
mfa model download acoustic english_us_arpa
mfa model download dictionary english_us_arpa

# Find MFA path for config
which mfa
```

### Custom Analysis Parameters

- **analysis_fps**: Higher values = more detailed analysis (10-100)
- **frame_rate**: Determines temporal resolution of features
- **output_directory**: Customize where results are saved

### MIDI Synchronization Tips

1. Ensure MIDI and audio are from the same performance
2. Check tempo alignment between files  
3. Use high-quality MIDI exports for best results

## Applications

The generated analysis data can be used for:

- 🎨 **Music Visualization**: Real-time audio-visual synchronization
- 🎮 **Rhythm Games**: Beat and onset detection for gameplay
- 📊 **Music Analysis**: Academic research and music information retrieval
- 🎬 **Video Production**: Synchronized effects and editing
- 🤖 **AI Training**: Feature extraction for machine learning models

## Troubleshooting

### Common Issues

**MFA not found**
```bash
conda activate neo_systema
which mfa  # Should show path
# Update config.yaml with correct mfa_executable_path
```

**MIDI timing seems off**
- Verify MIDI and audio are from the same recording
- Check tempo consistency between files
- Try different MIDI export settings

**Poor lyric alignment**
- Ensure audio quality is good (minimal reverb/noise)
- Check lyrics match exactly what's sung
- Try different MFA acoustic models
- Use manual timing as fallback

**GUI won't start**
- Check tkinter is available: `python -c "import tkinter"`
- Ensure all dependencies are installed
- Try command-line version first

### Dependency Status

Check what's available in your environment:

```python
# Test imports
try: import mido; print("✅ MIDI support available")
except: print("❌ MIDI support missing (pip install mido)")

try: import pygame; print("✅ Manual timing available") 
except: print("❌ Manual timing missing (pip install pygame)")
```

## Contributing

This project welcomes contributions! Areas for improvement:

- Additional audio backends (PyTorch, TensorFlow)
- More lyric alignment methods
- Extended MIDI analysis features
- Additional export formats
- Performance optimizations

## License

MIT License - See LICENSE file for details.

## Credits

Created by Sage Veda, Knowledge Architect (Claude 4.0)  
Built with librosa, numpy, and the scientific Python ecosystem.

---

*"Transforming audio into structured knowledge, one analysis at a time."*
