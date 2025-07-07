# Eldar Translate - Ancient Tongues of Middle-earth

A comprehensive translator for Tolkien's Elvish languages, featuring dictionary-based translation between English, Quenya, Sindarin, and Grey Company (RPG) with real-time auto-translation, comprehensive vocabulary from multiple scholarly sources, and **complete Tengwar script support**.

![Eldar Translate Interface](assets/preview.png)

## Features

- **🎯 Tengwar Script Translator**: Complete implementation of J.R.R. Tolkien's Tengwar writing system with authentic fonts
- **Real-time Auto-Translation**: Translates as you type with intelligent debouncing
- **Massive Vocabulary Database**: Over **50,000+ vocabulary entries** from Tolkien's works, Eldamo, Ardalambion, Hiswelókë, Quettaparma, and other scholarly sources
- **Comprehensive Linguistic Coverage**: 90,000+ total lines of linguistic data across multiple authoritative sources
- **Bidirectional Translation**: English ↔ Quenya, English ↔ Sindarin, and English ↔ Grey Company (RPG)
- **Advanced Tengwar System**: 5 authentic Tengwar fonts, 100+ letters/symbols, complete mode-specific rules
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
├── tengwar.html            # Tengwar script translator (NEW!)
├── js/
│   ├── app.js              # Main application logic & UI handling
│   ├── translator.js       # Core translation engine
│   ├── tengwar-translator.js # Tengwar script translation engine
│   └── tengwar-font-manager.js # Tengwar font management system
├── css/
│   └── tengwar-fonts.css   # Complete Tengwar font system
├── fonts/                  # Tengwar font files
│   ├── tngan*.ttf          # Tengwar Annatar font family
│   ├── tengwar-formal.ttf  # Tengwar Formal font
│   ├── tengwar-artano.ttf  # Tengwar Artano (Ring style)
│   └── tengwarfeanorregular.ttf # Tengwar Feanor font
├── tests/                  # Testing and validation files
│   ├── unicode-range-test.html # Unicode character support testing
│   ├── quick-font-test.html # Font loading and display testing
│   └── (other test files)  # Development and debugging tools
├── data/                   # Vocabulary databases
│   ├── comprehensive-expansion.json # Well-attested Tolkien vocabulary
│   ├── eldamo.json         # Eldamo comprehensive dictionary
│   ├── ardalambion.json    # Helge Fauskanger's Quenya wordlists
│   ├── hisweloke.json      # Sindarin & Noldorin dictionary
│   ├── tolkien-attested-vocabulary.json
│   ├── enhanced-vocabulary-expansion.json
│   ├── greycompany.json    # RPG/community vocabulary
│   ├── quenya-alphabet.json # Complete Quenya Tengwar alphabet
│   └── sindarin-alphabet.json # Complete Sindarin Tengwar alphabet
├── assets/                 # Images and resources
├── start-server.bat        # Windows batch script for easy server launch
└── README.md
```

## Data Sources

The translator uses vocabulary from multiple authoritative sources totaling **90,000+ lines of linguistic data**:

- **[Quettaparma](https://www.ambar-eldaron.com/telechargements/)** - Massive comprehensive lexicon (57,843 lines) - The most complete Elvish dictionary available
- **PDF-Parsed Vocabulary** - Extracted from academic publications (26,798 lines) - Scholarly Elvish dictionaries and grammars
- **[Eldamo](https://eldamo.org)** (CC-BY) - Comprehensive Neo-Eldarin lexicon (1,481 lines)
- **Master Alphabet** - Core vocabulary compilation (887 lines)
- **Hiswelókë** - Community Sindarin & Noldorin dictionary (679 lines)
- **Comprehensive Expansion** - Well-attested vocabulary from Tolkien's published works (586 lines)
- **Tolkien Attested Vocabulary** - Words directly from Tolkien's published works (335 lines)
- **Enhanced Vocabulary Expansion** - Scholarly reconstructions and domain-specific terms (243 lines)
- **Grey Company** - RPG and community vocabulary (244 lines) - Now selectable as separate language option
- **[Ardalambion](https://folk.uib.no/hnohf/)** - Helge Fauskanger's authoritative Quenya course (188 lines)
- **Elven Language Dictionary** - Additional scholarly sources (168 lines)

## Usage

### Basic Translation (index.html)

1. **Select Language**: Choose between Quenya, Sindarin, and Grey Company (RPG) using the radio buttons
2. **Type to Translate**: Enter English text in the source textarea - translation appears automatically
3. **Swap Direction**: Click the swap button or press `Ctrl/Cmd + Enter` to reverse translation direction
4. **Copy Results**: Click the copy button to copy translations to clipboard

### Tengwar Script Translation (tengwar.html)

1. **Access Tengwar Translator**: Click "Tengwar Translator" button from main page or navigate to `tengwar.html`
2. **Select Mode**: Choose between English, Quenya, or Sindarin writing modes
3. **Type to Convert**: Enter text in the left panel - Tengwar script appears automatically in the right panel
4. **View Beautiful Script**: Text renders in authentic Tengwar fonts with proper letter forms and tehtar (vowel marks)
5. **Copy Tengwar**: Copy the Tengwar script to use in documents or social media
6. **Try Examples**: Use the quick example buttons to see different translations

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

| English | Quenya | Sindarin | Tengwar (English Mode) |
|---------|--------|----------|------------------------|
| star | elen | êl | `E1;5` |
| friend | mellon | mellon | `b7|5$ |
| light | cala | galad | `j#j1 |
| tree | alda | galadh | `#mE6 |
| king | aran | aran | `#7E5 |
| queen | tári | bereth | `1;7% |

**Note**: Tengwar column shows actual Tengwar script when using the Tengwar translator page with proper fonts loaded.

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

- **Initial Load**: ~3-5 seconds (downloading massive 90,000+ line vocabulary databases)
- **Translation Speed**: Real-time with 500ms debounce for both Elvish and Tengwar translation
- **Memory Usage**: ~150-200MB for complete vocabulary dataset + Tengwar fonts
- **Tengwar Rendering**: Real-time script conversion with <50ms latency
- **Font Loading**: 5 Tengwar fonts with intelligent fallback system
- **Offline Support**: Full functionality after first load (including Tengwar fonts)

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

### ✅ Completed (July 7, 2025)
- [x] **Tengwar Support**: Complete Tengwar script translator with authentic fonts
- [x] **Advanced Font System**: Multi-font fallback system with 5 different Tengwar fonts
- [x] **Linguistic Accuracy**: Mode-specific rules for English, Quenya, and Sindarin
- [x] **Bidirectional Tengwar**: Convert both to and from Tengwar script

### 🚀 Future Features
- [ ] **v2.0**: Poetic word order and advanced grammar
- [ ] **Voice Input**: Speech-to-text translation
- [ ] **PWA Features**: Full offline mode with service worker
- [ ] **Mobile App**: React Native implementation
- [ ] **Advanced Morphology**: Verb conjugations and complex grammar rules
- [ ] **Tengwar Calligraphy Mode**: Handwriting-style Tengwar rendering

---

*"Not all those who wander are lost."* - J.R.R. Tolkien

**Major Update: July 7, 2025** - Complete Tengwar script implementation achieved!

Created with ancient wisdom by [Lackadaisical Security](https://github.com/Lackadaisical-Security) © 2025 