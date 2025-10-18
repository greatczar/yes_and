# 🎭 Yes, And — Multi-Agent Improv Game

An interactive improv game powered by multiple AI language models that work together to create spontaneous, collaborative stories based on the classic improv principle of "Yes, And."

## Overview

This project brings together three different AI models to perform an improv scene:
- **Drew** (GPT-4o-mini) - The Host who guides the game
- **Ryan** (Gemini 2.5 Flash) - Player 1
- **Wayne** (Claude 3.5 Haiku) - Player 2

The host manages the game flow while the two players improvise a scene based on scenarios provided by the user, following the fundamental improv rule: always accept what has been established ("Yes") and add something new ("And").

## Features

- **Multi-Agent Collaboration**: Three different AI models working together in real-time
- **Interactive Web Interface**: Built with Gradio for easy interaction
- **Live Streaming**: Watch the improv scene unfold in real-time
- **Colorful Transcript**: Each performer has their own color-coded display
- **Configurable Rounds**: Adjust the maximum number of turns
- **Smart Host**: The host decides when to continue or end the scene based on the flow

## Prerequisites

- Python 3.8+
- API keys for:
  - OpenAI (for GPT-4o-mini)
  - Google AI (for Gemini)
  - Anthropic (for Claude)

## Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/yes_and.git
cd yes_and
```

2. Install dependencies:
```bash
pip install openai gradio python-dotenv
```

3. Create a `.env` file in the project root with your API keys:
```env
OPENAI_API_KEY=your_openai_api_key_here
GOOGLE_API_KEY=your_google_api_key_here
ANTHROPIC_API_KEY=your_anthropic_api_key_here
```

## Usage

1. Open the notebook `src/yes_and_v1.ipynb` in Jupyter

2. Run all cells to initialize the performers and launch the Gradio interface

3. The web interface will open automatically in your browser

4. Interact with Drew (the host) to describe a scenario

5. Once the host says `[HOST DECISION: Start Game]`, the performers will begin improvising

6. Watch the scene unfold in the Game Transcript panel

7. Click "New Game" to start fresh with a new scenario

## How It Works

### The Performers

Each performer is an instance of the `Performer` class with:
- Unique identity (name, role)
- AI model configuration
- System prompts that define their behavior
- Shared conversation history

### The Game Flow

1. **Setup Phase**: User chats with Drew (host) to establish the scenario
2. **Scene Brief**: Drew converts the scenario into structured instructions for the players
3. **Improv Loop**: Players alternate turns, each adding to the scene
4. **Host Decisions**: After each pair of turns, Drew decides whether to continue or end
5. **Closing**: When ending, Drew provides a closing message

### Key Features

- **None-Content Handling**: Gracefully handles API errors or empty responses
- **Turn Management**: Ensures players only speak on their turn and don't play other characters
- **Visual Feedback**: Color-coded transcript with emojis for easy reading:
  - 🎭 **Blue**: Drew (Host)
  - 🎪 **Green**: Ryan (Player 1)
  - 🎨 **Purple**: Wayne (Player 2)

## Configuration

### Adjust Max Rounds
Use the slider in the interface (default: 6, range: 5-10)

### Change Models
Edit the performer configurations in the notebook:
```python
host = Performer(
    name="Drew",
    role="host", 
    client_config={"api_key": os.getenv('OPENAI_API_KEY')}, 
    model="gpt-4o-mini"
)
```

### Modify Prompts
System prompts can be customized to change performer behavior and personality.

## Technical Details

### Architecture
- **Dataclass-based Design**: Uses Python dataclasses for clean performer configuration
- **Shared History**: All performers share a common conversation history
- **Streaming Generator**: Game transcript streams in real-time using Python generators
- **Message Format**: Uses OpenAI-style message dictionaries with 'role' and 'content' keys

### API Compatibility
The project uses OpenAI's client library with custom base URLs to support multiple providers:
- Anthropic API via OpenAI-compatible endpoint
- Google Gemini via OpenAI-compatible endpoint
- Native OpenAI API

## Troubleshooting

### No Response Generated
If you see `[No response generated]`, check:
- API keys are valid and have available credits
- Network connection is stable
- Model names are correct

### Players Speaking for Each Other
The system prompts have been carefully tuned to prevent this, but if it happens:
- Try adjusting the temperature (default: 0.7)
- Modify the CRITICAL RULES in the system prompts

## Future Enhancements

- [ ] Add more performers for larger ensemble scenes
- [ ] Support for different improv games beyond "Yes, And"
- [ ] Save and replay favorite scenes
- [ ] Audience voting on scene quality
- [ ] Export transcripts in various formats

## License

[Add your license here]

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Acknowledgments

- Built with [Gradio](https://gradio.app/)
- Powered by OpenAI, Anthropic, and Google AI models
- Inspired by the timeless art of improvisational theater

---

**Note**: This project requires active API keys for three different AI providers. API usage will incur costs based on each provider's pricing.

