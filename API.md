# Eldar Translate API Documentation

Complete API reference for integrating the Eldar Translate engine into your applications.

## Table of Contents

- [Quick Start](#quick-start)
- [Core Classes](#core-classes)
- [VocabularyLoader](#vocabularyloader)
- [EldarTranslator](#eldartranslator)
- [Data Structures](#data-structures)
- [Integration Examples](#integration-examples)
- [Error Handling](#error-handling)
- [Performance Considerations](#performance-considerations)

## Quick Start

```javascript
import { EldarTranslator } from './js/translator.js';

// Initialize translator
const translator = new EldarTranslator();
await translator.initialize();

// Set language and direction
translator.setLanguage('quenya');
translator.setDirection('to-elvish');

// Translate text
const result = translator.translate('star friend');
console.log(result); // "elen mellon"
```

## Core Classes

### VocabularyLoader

Manages loading and merging of vocabulary databases from multiple sources.

#### Constructor

```javascript
const loader = new VocabularyLoader();
```

#### Methods

##### `loadAllVocabularies()`

Loads and merges all vocabulary files from the data directory.

```javascript
const vocabulary = await loader.loadAllVocabularies();
```

**Returns:** `Promise<Object>` - Complete vocabulary database

**Structure:**
```javascript
{
  quenya: { [word]: VocabularyEntry },
  sindarin: { [word]: VocabularyEntry },
  greycompany: { [word]: VocabularyEntry },
  englishToQuenya: { [english]: Array<Translation> },
  englishToSindarin: { [english]: Array<Translation> },
  englishToGreycompany: { [english]: Array<Translation> },
  metadata: {
    sources: Array<string>,
    totalEntries: number,
    loadTime: string
  }
}
```

##### `getVocabulary()`

Returns cached vocabulary data.

```javascript
const vocabulary = loader.getVocabulary();
```

**Returns:** `Object` - Cached vocabulary database

### EldarTranslator

Main translation engine with morphological analysis and dictionary lookup.

#### Constructor

```javascript
const translator = new EldarTranslator();
```

#### Methods

##### `initialize()`

Initializes the translator by loading vocabulary databases.

```javascript
await translator.initialize();
```

**Returns:** `Promise<boolean>` - Success status

##### `setLanguage(language)`

Sets the target Elvish language.

```javascript
translator.setLanguage('quenya');
```

**Parameters:**
- `language` (string): 'quenya', 'sindarin', or 'greycompany'

##### `setDirection(direction)`

Sets translation direction.

```javascript
translator.setDirection('to-elvish');
```

**Parameters:**
- `direction` (string): 'to-elvish' or 'to-english'

##### `translate(text)`

Translates text using dictionary lookup and morphological rules.

```javascript
const result = translator.translate('star friend');
```

**Parameters:**
- `text` (string): Text to translate

**Returns:** `string` - Translated text

##### `searchDictionary(query, language)`

Searches vocabulary database for matching entries.

```javascript
const results = translator.searchDictionary('star', 'quenya');
```

**Parameters:**
- `query` (string): Search term
- `language` (string): 'quenya', 'sindarin', 'greycompany', or 'all'

**Returns:** `Array<SearchResult>` - Matching dictionary entries

##### `getStats()`

Returns translator statistics.

```javascript
const stats = translator.getStats();
```

**Returns:** `Object` - Statistics object

```javascript
{
  totalWords: number,
  quenya: number,
  sindarin: number,
  greycompany: number,
  sources: Array<string>,
  isReady: boolean
}
```

#### Properties

##### `isReady`

Boolean indicating if translator is initialized and ready.

```javascript
if (translator.isReady) {
  // Ready to translate
}
```

##### `currentLanguage`

Current target language ('quenya', 'sindarin', 'greycompany').

##### `currentDirection`

Current translation direction ('to-elvish', 'to-english').

## Data Structures

### VocabularyEntry

Structure for individual vocabulary entries.

```javascript
{
  meanings: Array<string>,        // Array of English meanings
  pos: string,                    // Part of speech
  etymology?: string,             // Etymological information
  notes?: string,                 // Additional notes
  plural?: string,                // Plural form
  priority: number,               // Source priority (higher = more reliable)
  source: string,                 // Source identifier
  confidence: string              // Confidence level
}
```

### Translation

Structure for reverse lookup translations.

```javascript
{
  word: string,                   // Elvish word
  entry: VocabularyEntry         // Full vocabulary entry
}
```

### SearchResult

Structure for dictionary search results.

```javascript
{
  word: string,                   // Elvish word
  language: string,               // Language identifier
  entry: VocabularyEntry,         // Full vocabulary entry
  relevance: number               // Search relevance score (0-100)
}
```

## Integration Examples

### Basic Web Integration

```html
<!DOCTYPE html>
<html>
<head>
    <script type="module">
        import { EldarTranslator } from './js/translator.js';
        
        const translator = new EldarTranslator();
        await translator.initialize();
        
        document.getElementById('translateBtn').onclick = () => {
            const input = document.getElementById('input').value;
            const result = translator.translate(input);
            document.getElementById('output').textContent = result;
        };
    </script>
</head>
<body>
    <input id="input" placeholder="Enter text">
    <button id="translateBtn">Translate</button>
    <div id="output"></div>
</body>
</html>
```

### Node.js Integration

```javascript
// Mock fetch for Node.js
global.fetch = async (url) => {
    const fs = require('fs');
    const path = require('path');
    const data = fs.readFileSync(path.join(__dirname, url), 'utf8');
    return { ok: true, json: async () => JSON.parse(data) };
};

// Load translator
const translatorCode = fs.readFileSync('./js/translator.js', 'utf8');
const nodeCode = translatorCode.replace(/export\s*\{[^}]+\};\s*$/, '');
eval(nodeCode);

// Use translator
const translator = new EldarTranslator();
await translator.initialize();
console.log(translator.translate('hello world'));
```

### React Integration

```jsx
import React, { useState, useEffect } from 'react';
import { EldarTranslator } from './js/translator.js';

function TranslatorComponent() {
    const [translator, setTranslator] = useState(null);
    const [input, setInput] = useState('');
    const [output, setOutput] = useState('');
    
    useEffect(() => {
        const initTranslator = async () => {
            const t = new EldarTranslator();
            await t.initialize();
            setTranslator(t);
        };
        initTranslator();
    }, []);
    
    const handleTranslate = () => {
        if (translator) {
            setOutput(translator.translate(input));
        }
    };
    
    return (
        <div>
            <input value={input} onChange={(e) => setInput(e.target.value)} />
            <button onClick={handleTranslate}>Translate</button>
            <div>{output}</div>
        </div>
    );
}
```

## Error Handling

### Common Errors

```javascript
try {
    await translator.initialize();
} catch (error) {
    if (error.message.includes('Failed to load')) {
        console.error('Network error loading vocabularies');
    }
}

// Check readiness before translation
if (!translator.isReady) {
    console.error('Translator not initialized');
    return;
}

// Handle empty translations
const result = translator.translate('nonexistent word');
if (result.includes('[') && result.includes(']')) {
    console.log('Translation not found');
}
```

### Custom Error Handling

```javascript
class TranslationError extends Error {
    constructor(message, code) {
        super(message);
        this.name = 'TranslationError';
        this.code = code;
    }
}

// Wrapper with enhanced error handling
async function safeTranslate(text) {
    try {
        if (!translator.isReady) {
            throw new TranslationError('Translator not ready', 'NOT_READY');
        }
        
        const result = translator.translate(text);
        
        if (!result || result.trim() === '') {
            throw new TranslationError('Empty translation result', 'EMPTY_RESULT');
        }
        
        return result;
    } catch (error) {
        console.error('Translation failed:', error);
        throw error;
    }
}
```

## Performance Considerations

### Optimization Tips

1. **Initialize Once**: Create a single translator instance and reuse it
2. **Batch Operations**: Process multiple translations in sequence rather than parallel
3. **Cache Results**: Store frequently translated phrases
4. **Lazy Loading**: Only load specific language vocabularies if needed

### Memory Management

```javascript
// Check memory usage
const stats = translator.getStats();
console.log(`Loaded ${stats.totalWords} words from ${stats.sources.length} sources`);

// The translator loads ~50-100MB of vocabulary data
// Consider this when deploying to memory-constrained environments
```

### Performance Monitoring

```javascript
// Measure translation performance
const startTime = performance.now();
const result = translator.translate('long text to translate');
const endTime = performance.now();
console.log(`Translation took ${endTime - startTime} milliseconds`);
```

## Advanced Usage

### Custom Vocabulary Sources

```javascript
// Add custom vocabulary to existing loader
const customVocab = {
    quenya: {
        'custom-word': {
            meanings: ['custom meaning'],
            pos: 'noun',
            priority: 200,
            source: 'custom',
            confidence: 'high'
        }
    }
};

// This would require extending the VocabularyLoader class
```

### Morphological Analysis

```javascript
// Access morphological analysis results
const analysis = translator._analyzeEnglishMorphology('stars');
console.log(analysis); // { baseWord: 'star', isPlural: true }

// Apply Elvish morphological rules
const plural = translator._makeElvishPlural('elen', { source: 'quenya' });
console.log(plural); // 'eleni'
```

### Dictionary Search with Filters

```javascript
// Advanced dictionary search
const results = translator.searchDictionary('star', 'all');
const highConfidence = results.filter(r => r.entry.confidence === 'very_high');
const tolkienAttested = results.filter(r => r.entry.source === 'tolkien-attested');
```

## Browser Compatibility

- **Modern ES6+ browsers**: Chrome 61+, Firefox 60+, Safari 12+, Edge 79+
- **Module support**: Must be served over HTTP (not file://)
- **Local storage**: Optional for caching (graceful fallback)

## File Structure Requirements

```
your-project/
├── js/
│   ├── translator.js      # Core translator engine
│   └── app.js            # UI integration (optional)
├── data/                 # Vocabulary databases
│   ├── eldamo.json
│   ├── ardalambion.json
│   └── [other vocabulary files]
└── debug-pronouns.json   # High-priority vocabulary fixes
```

## License and Attribution

When using the Eldar Translate API:

1. **Include MIT License** from the main project
2. **Attribute vocabulary sources** as specified in THIRD_PARTY_LICENSES.md
3. **Maintain educational use** principles
4. **Credit linguistic sources** in your application

---

For more information, see the main [README.md](README.md) and [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md) files. 