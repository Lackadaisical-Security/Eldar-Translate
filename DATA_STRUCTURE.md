# Data Structure Documentation

Complete specification of vocabulary file formats and data structures used in Eldar Translate.

## Overview

Eldar Translate uses a flexible JSON-based vocabulary system that merges multiple linguistic sources with priority-based precedence. This document describes the data structures and file formats used throughout the system.

## Vocabulary File Format

### Basic Structure

All vocabulary files follow this general JSON structure:

```json
{
  "metadata": {
    "name": "Source Name",
    "description": "Description of the source",
    "version": "1.0.0",
    "priority": 100,
    "source_type": "scholarly|community|reconstructed",
    "languages": ["quenya", "sindarin", "greycompany"]
  },
  "quenya": {
    "word": VocabularyEntry,
    "another-word": VocabularyEntry
  },
  "sindarin": {
    "word": VocabularyEntry,
    "another-word": VocabularyEntry
  },
  "greycompany": {
    "word": VocabularyEntry,
    "another-word": VocabularyEntry
  }
}
```

### VocabularyEntry Structure

Each vocabulary entry follows this structure:

```json
{
  "meanings": ["meaning1", "meaning2", "meaning3"],
  "pos": "noun|verb|adjective|adverb|preposition|conjunction|pronoun|number|quantifier",
  "etymology": "optional etymological information",
  "notes": "optional additional notes",
  "plural": "optional plural form",
  "priority": 100,
  "source": "source_identifier",
  "confidence": "very_high|high|moderate|low"
}
```

#### Field Descriptions

- **meanings** (required): Array of English meanings/translations
- **pos** (optional): Part of speech classification
- **etymology** (optional): Etymological information and root analysis
- **notes** (optional): Additional linguistic or usage notes
- **plural** (optional): Irregular plural form if applicable
- **priority** (required): Numeric priority (higher = more reliable)
- **source** (required): Source identifier for attribution
- **confidence** (required): Confidence level in the translation

## Source Priority System

The system uses a priority-based merging system where higher priority sources override lower priority ones:

| Priority | Source Type | Description |
|----------|-------------|-------------|
| 150 | Debug/Critical | Essential fixes and critical vocabulary |
| 110-120 | Scholarly Primary | Peer-reviewed academic sources |
| 90-100 | Scholarly Secondary | Well-researched community sources |
| 70-89 | Community Scholarly | Community-maintained dictionaries |
| 60-69 | Community Practical | RPG and creative writing sources |
| 50-59 | Experimental | Unverified or speculative entries |

## Specific File Formats

### debug-pronouns.json

High-priority vocabulary fixes and essential words:

```json
{
  "metadata": {
    "name": "Debug Basic Pronouns & Morphological Analysis",
    "priority": 150,
    "description": "Essential pronouns and morphological forms that must work correctly"
  },
  "quenya": {
    "ninya": {
      "meanings": ["my"],
      "pos": "possessive",
      "priority": 150
    }
  },
  "sindarin": {
    "nín": {
      "meanings": ["my"],
      "pos": "possessive",
      "priority": 150
    }
  }
}
```

### comprehensive-expansion.json

Well-attested vocabulary from Tolkien's works:

```json
{
  "metadata": {
    "name": "Comprehensive Tolkien Vocabulary Expansion",
    "priority": 110,
    "description": "Well-attested vocabulary from Tolkien's published works and scholarly reconstructions"
  },
  "quenya": {
    "Elentári": {
      "meanings": ["star-queen", "Varda"],
      "pos": "noun",
      "etymology": "elen 'star' + tári 'queen'",
      "priority": 110,
      "source": "comprehensive",
      "confidence": "very_high"
    }
  }
}
```

### eldamo.json

Comprehensive linguistic database format:

```json
{
  "quenya": {
    "elen": {
      "meanings": ["star"],
      "pos": "noun",
      "etymology": "√EL 'star'",
      "notes": "Q. elen, S. êl, primitive *elen",
      "plural": "eleni",
      "priority": 90,
      "source": "eldamo",
      "confidence": "high"
    }
  }
}
```

### ardalambion.json

Helge Fauskanger's academic analysis format:

```json
{
  "quenya": {
    "mellon": {
      "meanings": ["friend"],
      "pos": "noun",
      "etymology": "√MEL 'to love'",
      "notes": "Fauskanger: Common word for friend, cognate with Sindarin mellon",
      "priority": 100,
      "source": "ardalambion",
      "confidence": "very_high"
    }
  }
}
```

### Enhanced Vocabulary Format

For domain-specific vocabulary:

```json
{
  "vocabulary_domains": {
    "nature": {
      "quenya": {
        "alda": {
          "meanings": ["tree"],
          "pos": "noun",
          "priority": 70,
          "source": "enhanced",
          "confidence": "moderate"
        }
      }
    },
    "characters": {
      "quenya": {
        "Elrond": {
          "meanings": ["star-dome", "Elrond"],
          "pos": "proper noun",
          "etymology": "êl 'star' + rond 'dome'",
          "priority": 70,
          "source": "enhanced",
          "confidence": "very_high"
        }
      }
    }
  }
}
```

## Data Validation Rules

### Required Fields

- Every vocabulary entry must have `meanings` (array)
- Every vocabulary entry must have `priority` (number)
- Every vocabulary entry must have `source` (string)
- Every vocabulary entry must have `confidence` (string)

### Validation Rules

1. **Meanings**: Must be non-empty array of strings
2. **Priority**: Must be integer between 1-200
3. **Source**: Must match a known source identifier
4. **Confidence**: Must be one of: very_high, high, moderate, low
5. **POS**: If present, must be valid part of speech
6. **Etymology**: If present, must be non-empty string
7. **Plural**: If present, must be non-empty string

### Example Validation

```javascript
function validateVocabularyEntry(entry) {
  const errors = [];
  
  if (!Array.isArray(entry.meanings) || entry.meanings.length === 0) {
    errors.push('meanings must be non-empty array');
  }
  
  if (typeof entry.priority !== 'number' || entry.priority < 1 || entry.priority > 200) {
    errors.push('priority must be number between 1-200');
  }
  
  if (!['very_high', 'high', 'moderate', 'low'].includes(entry.confidence)) {
    errors.push('confidence must be valid level');
  }
  
  return errors;
}
```

## Runtime Data Structures

### Merged Vocabulary Structure

After loading and merging, the vocabulary is structured as:

```javascript
{
  // Direct language lookups
  quenya: {
    "word": VocabularyEntry,
    // ... all Quenya words
  },
  sindarin: {
    "word": VocabularyEntry,
    // ... all Sindarin words
  },
  greycompany: {
    "word": VocabularyEntry,
    // ... all Grey Company words
  },
  
  // Reverse lookups (English -> Elvish)
  englishToQuenya: {
    "english-word": [
      { word: "quenya-word", entry: VocabularyEntry },
      // ... sorted by priority
    ]
  },
  englishToSindarin: {
    "english-word": [
      { word: "sindarin-word", entry: VocabularyEntry },
      // ... sorted by priority
    ]
  },
  englishToGreycompany: {
    "english-word": [
      { word: "greycompany-word", entry: VocabularyEntry },
      // ... sorted by priority
    ]
  },
  
  // Metadata
  metadata: {
    sources: ["debug-pronouns", "comprehensive", "eldamo", ...],
    totalEntries: 6500,
    loadTime: "2024-01-01T00:00:00.000Z",
    version: "2.0.0"
  }
}
```

### Search Result Structure

Dictionary search results follow this format:

```javascript
{
  word: "elen",
  language: "quenya",
  entry: {
    meanings: ["star"],
    pos: "noun",
    etymology: "√EL 'star'",
    priority: 90,
    source: "eldamo",
    confidence: "high"
  },
  relevance: 100  // 0-100 based on search match quality
}
```

## Creating New Vocabulary Files

### Step 1: Create Base Structure

```json
{
  "metadata": {
    "name": "Your Source Name",
    "description": "Description of your vocabulary source",
    "version": "1.0.0",
    "priority": 75,
    "source_type": "community",
    "languages": ["quenya", "sindarin"],
    "author": "Your Name",
    "date": "2024-01-01"
  },
  "quenya": {},
  "sindarin": {}
}
```

### Step 2: Add Vocabulary Entries

```json
{
  "quenya": {
    "your-word": {
      "meanings": ["english meaning"],
      "pos": "noun",
      "etymology": "optional etymology",
      "priority": 75,
      "source": "your-source-id",
      "confidence": "moderate"
    }
  }
}
```

### Step 3: Update Loader

Add your file to the vocabulary loader in `js/translator.js`:

```javascript
const [eldamo, tolkienAttested, enhanced, ardalambion, hisweloke, greycompany, comprehensive, debugPronouns, yourFile] = await Promise.all([
  // ... existing files
  this._loadJSON('data/your-vocabulary.json')
]);

// Add to merge with appropriate priority
{ data: yourFile, priority: 75, source: 'your-source-id' }
```

## Performance Considerations

### File Size Limits

- Individual files should be under 2MB for optimal loading
- Total vocabulary database is ~5-10MB
- Browser memory usage is ~50-100MB after loading

### Optimization Tips

1. **Minimize redundancy**: Don't duplicate entries across files
2. **Use priorities**: Let higher priority sources override lower ones
3. **Compress entries**: Remove unnecessary whitespace
4. **Cache effectively**: Structure for efficient lookups

### Memory Usage

```javascript
// Monitor memory usage
const stats = translator.getStats();
console.log(`Total entries: ${stats.totalWords}`);
console.log(`Memory estimate: ${stats.totalWords * 200} bytes`);
```

## File Naming Conventions

- Use kebab-case for file names: `my-vocabulary.json`
- Include source type in name: `scholarly-quenya.json`
- Version files appropriately: `eldamo-v2.json`
- Use descriptive names: `tolkien-attested-vocabulary.json`

## Common Issues and Solutions

### Issue: JSON Syntax Errors
- Use JSON validator before adding files
- Check for trailing commas, missing quotes
- Validate with `JSON.parse()` test

### Issue: Priority Conflicts
- Use established priority ranges
- Document priority decisions
- Test with priority viewer

### Issue: Character Encoding
- Save files as UTF-8
- Handle diacritics properly
- Test special characters

## Migration Guide

### From Version 1.0 to 2.0

1. Update metadata structure
2. Add confidence levels
3. Standardize priority ranges
4. Add source attribution

### Example Migration

```javascript
// Old format
{
  "elen": "star"
}

// New format
{
  "elen": {
    "meanings": ["star"],
    "pos": "noun",
    "priority": 90,
    "source": "eldamo",
    "confidence": "high"
  }
}
```

---

This documentation should be updated when the vocabulary format changes or new features are added to the data structure system. 