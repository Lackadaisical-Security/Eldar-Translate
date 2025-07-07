# Eldar Translate - Ancient Tongues of Middle-earth

A comprehensive translator for Tolkien's Elvish languages, featuring dictionary-based translation between English, Quenya, Sindarin, and Grey Company (RPG) with real-time auto-translation and comprehensive vocabulary from multiple scholarly sources.

![Eldar Translate Interface](assets/preview.png)

## Features

- **Real-time Auto-Translation**: Translates as you type with intelligent debouncing
- **Comprehensive Vocabulary**: Over 5,000+ words from Tolkien's works, Eldamo, Ardalambion, Hiswelókë, and other scholarly sources
- **Bidirectional Translation**: English ↔ Quenya, English ↔ Sindarin, and English ↔ Grey Company (RPG)
- **Master Alphabet Browser**: Search comprehensive word database with etymology and source attribution
- **Morphological Intelligence**: Basic plural forms and linguistic pattern recognition
- **Beautiful Middle-earth Theme**: Authentic parchment manuscript aesthetic
- **Offline-Ready**: Works offline after first load (vocabulary cached in browser)

## Quick Start

### Option 1: Windows Batch Script (Easiest)
```bash
# Simply double-click the batch file
start-server.bat

# Or run from command line
start-server.bat
```

### Option 2: Python (Recommended)
```bash
# Navigate to project directory
cd Eldar-Translate

# Start server on port 3015
python -m http.server 3015

# Open in browser
open http://localhost:3015
```

### Option 3: Node.js
```bash
# Install a simple HTTP server
npm install -g http-server

# Navigate to project directory
cd Eldar-Translate

# Start server on port 3015
http-server -p 3015

# Open in browser
open http://localhost:3015
```

### Option 4: PHP
```bash
# Navigate to project directory
cd Eldar-Translate

# Start PHP built-in server on port 3015
php -S localhost:3015

# Open in browser
open http://localhost:3015
```

### Option 5: Live Server (VS Code Extension)
1. Install the "Live Server" extension in VS Code
2. Right-click on `index.html`
3. Select "Open with Live Server"
4. Modify the URL to use port 3015 in extension settings

## Project Structure

```
Eldar-Translate/
├── index.html              # Main application interface
├── js/
│   ├── app.js              # Main application logic & UI handling
│   └── translator.js       # Core translation engine
├── data/                   # Vocabulary databases
│   ├── comprehensive-expansion.json # Well-attested Tolkien vocabulary
│   ├── eldamo.json         # Eldamo comprehensive dictionary
│   ├── ardalambion.json    # Helge Fauskanger's Quenya wordlists
│   ├── hisweloke.json      # Sindarin & Noldorin dictionary
│   ├── tolkien-attested-vocabulary.json
│   ├── enhanced-vocabulary-expansion.json
│   └── greycompany.json    # RPG/community vocabulary
├── assets/                 # Images and resources
├── start-server.bat        # Windows batch script for easy server launch
└── README.md
```

## Data Sources

The translator uses vocabulary from multiple authoritative sources:

- **Comprehensive Expansion** - Well-attested vocabulary from Tolkien's published works and scholarly reconstructions
- **[Eldamo](https://eldamo.org)** (CC-BY) - Comprehensive Neo-Eldarin lexicon
- **[Ardalambion](https://folk.uib.no/hnohf/)** - Helge Fauskanger's authoritative Quenya course
- **Hiswelókë** - Community Sindarin & Noldorin dictionary
- **Tolkien Attested Vocabulary** - Words directly from Tolkien's published works
- **Enhanced Vocabulary Expansion** - Scholarly reconstructions and domain-specific terms
- **Grey Company** - RPG and community vocabulary (now selectable as separate language option)

## Usage

### Basic Translation

1. **Select Language**: Choose between Quenya, Sindarin, and Grey Company (RPG) using the radio buttons
2. **Type to Translate**: Enter English text in the source textarea - translation appears automatically
3. **Swap Direction**: Click the swap button or press `Ctrl/Cmd + Enter` to reverse translation direction
4. **Copy Results**: Click the copy button to copy translations to clipboard

### Master Alphabet Browser

1. **Search Words**: Type English or Elvish words in the search box
2. **Filter by Language**: Use the dropdown to filter results by Quenya, Sindarin, Grey Company (RPG), or all languages
3. **View Details**: Each result shows meanings, etymology, part of speech, and source attribution
4. **Confidence Levels**: 
   - **Very High**: Directly attested in Tolkien's texts
   - **High**: Scholarly reconstruction from reliable sources
   - **Moderate**: Community accepted forms
   - **Low**: Experimental or disputed forms

### Translation Examples

| English | Quenya | Sindarin |
|---------|--------|----------|
| star | elen | êl |
| friend | mellon | mellon |
| light | cala | galad |
| tree | alda | galadh |
| king | aran | aran |
| queen | tári | bereth |

## Advanced Features

### Morphological Rules

The translator includes basic morphological intelligence:

**Quenya Plurals:**
- Words ending in vowels: add `-r` (elen → elenr)
- Words ending in consonants: add `-i` (atan → atani)

**Sindarin Plurals:**
- Default: add `-in` (adan → edain)
- Irregular forms preserved from dictionary data

### Keyboard Shortcuts

- `Ctrl/Cmd + Enter`: Swap translation direction
- Auto-translation with 500ms debounce delay
- Real-time character counting

## Technical Details

### Browser Requirements

- **Modern ES6+ Browser**: Chrome 61+, Firefox 60+, Safari 12+, Edge 79+
- **JavaScript Modules**: Must be served over HTTP (not file://)
- **Local Storage**: Used for vocabulary caching (optional)

### Performance

- **Initial Load**: ~2-3 seconds (downloading vocabulary databases)
- **Translation Speed**: Real-time with 500ms debounce
- **Memory Usage**: ~50-100MB for full vocabulary dataset
- **Offline Support**: Full functionality after first load

### Architecture

- **Modular ES6**: Clean separation between translation engine and UI
- **Dictionary-Based**: Pure lexicon lookup with morphological rules
- **Priority System**: Higher-quality sources take precedence
- **Extensible**: Easy to add new vocabulary sources

## Development

### Adding New Vocabulary

1. Create new JSON file in `data/` directory
2. Follow existing format with `meanings`, `pos`, `etymology`, etc.
3. Update `VocabularyLoader` in `translator.js` to include new source
4. Set appropriate priority level for quality ranking

### Customizing Morphology

Edit the morphological rules in `translator.js`:
- `_analyzeEnglishMorphology()`: English word analysis
- `_makeElvishPlural()`: Elvish plural formation
- `_generateAlternativeSpellings()`: Diacritic handling

## License

MIT License - See LICENSE file for details

This project is not affiliated with Middle-earth Enterprises or the Tolkien Estate. Vocabulary data is used under CC-BY licenses where applicable.

## Credits

- **Vocabulary Sources**: Eldamo.org, Ardalambion, Hiswelókë, and the Tolkien linguistic community
- **Design Inspiration**: Medieval manuscripts and Middle-earth aesthetics
- **Fonts**: Cinzel, EB Garamond (Google Fonts)
- **Icons**: Lucide React
- **Framework**: Tailwind CSS

## Documentation

- **[API Documentation](API.md)** - Complete API reference for developers
- **[Troubleshooting Guide](TROUBLESHOOTING.md)** - Common issues and solutions
- **[Data Structure Documentation](DATA_STRUCTURE.md)** - Vocabulary file formats and structures
- **[Third-Party Licenses](THIRD_PARTY_LICENSES.md)** - Complete licensing information

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly with various translations
5. Submit a pull request

### Reporting Issues

Please include:
- Browser version and OS
- Steps to reproduce
- Expected vs actual translation results
- Console error messages (if any)

For common issues, check the [Troubleshooting Guide](TROUBLESHOOTING.md) first.

## Roadmap

- [ ] **v2.0**: Poetic word order and advanced grammar
- [ ] **Tengwar Support**: Display translations in Tengwar script
- [ ] **Voice Input**: Speech-to-text translation
- [ ] **PWA Features**: Full offline mode with service worker
- [ ] **Mobile App**: React Native implementation
- [ ] **Advanced Morphology**: Verb conjugations and complex grammar rules

---

*"Not all those who wander are lost."* - J.R.R. Tolkien

Created with ancient wisdom by [Lackadaisical Security](https://github.com/Lackadaisical-Security) © 2025 