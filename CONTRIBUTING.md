# Contributing to Eldar-Translate

Thank you for your interest in contributing to Eldar-Translate! This project is a comprehensive semantic translation system for Tolkien's Elvish languages (Quenya and Sindarin). We welcome contributions from linguists, developers, researchers, and Tolkien enthusiasts.

## 🌟 **What We're Building**

Eldar-Translate is a scholarly tool for studying Tolkien's Elvish languages (Quenya and Sindarin), featuring:

- **Extensive vocabulary database** compiled from multiple scholarly sources
- **Semantic analysis** for context-aware translation attempts
- **Morphological patterns** based on attested forms and reconstructions
- **Research-grade quality** with ongoing validation and improvement
- **Self-contained architecture** for educational and research use

## 📋 **Table of Contents**

- [Getting Started](#getting-started)
- [Types of Contributions](#types-of-contributions)
- [Development Setup](#development-setup)
- [Coding Standards](#coding-standards)
- [Linguistic Data Contributions](#linguistic-data-contributions)
- [Testing Guidelines](#testing-guidelines)
- [Pull Request Process](#pull-request-process)
- [Issue Reporting](#issue-reporting)
- [Community Guidelines](#community-guidelines)

## 🚀 **Getting Started**

### Prerequisites

- **JavaScript Knowledge**: Familiarity with modern JavaScript (ES6+)
- **Linguistic Interest**: Understanding of or willingness to learn about Tolkien's languages
- **Git**: Basic Git workflow knowledge
- **Node.js**: For running tests and development tools (optional)

### Quick Start

1. **Fork the repository**
   ```bash
   git clone https://github.com/your-username/Eldar-Translate.git
   cd Eldar-Translate
   ```

2. **Set up development environment**
   ```bash
   # Start the development server
   python -m http.server 3015
   # or use the batch file on Windows
   start-server.bat
   ```

3. **Run tests**
   ```bash
   # Open tests/comprehensive-test-suite.js in browser
   # or run via Node.js if available
   ```

## 🎯 **Types of Contributions**

### **1. Linguistic Data Contributions**

#### **Vocabulary Additions**
- **New translation entries** for English words/phrases
- **Source attribution** with proper citations
- **Priority weighting** based on authenticity
- **Semantic domain classification**

#### **Grammar and Morphology**
- **Inflection patterns** for Quenya and Sindarin
- **Mutation rules** for Sindarin
- **Compound formation** patterns
- **Etymological analysis**

#### **Semantic Domains**
- **Thematic categorization** of vocabulary
- **Context-aware translation** improvements
- **Domain-specific terminology**

### **2. Code Contributions**

#### **Core Engine Improvements**
- **Performance optimizations** in translation algorithms
- **Memory usage** improvements
- **Caching strategies** enhancement
- **Error handling** and validation

#### **Advanced Features**
- **New linguistic features** (tenses, moods, etc.)
- **UI/UX improvements** for the web interface
- **API enhancements** for integration
- **Testing framework** improvements

#### **Documentation**
- **API documentation** updates
- **User guides** and tutorials
- **Code comments** and explanations
- **Translation examples** and use cases

### **3. Testing and Quality Assurance**

#### **Test Development**
- **Unit tests** for individual functions
- **Integration tests** for system components
- **Accuracy tests** for translation quality
- **Performance benchmarks**

#### **Quality Validation**
- **Source verification** against Tolkien texts and scholarly works
- **Cross-reference checking** with established linguistic resources
- **Edge case testing** for unusual inputs
- **Regression testing** for existing functionality

## 🛠️ **Development Setup**

### **Project Structure**

```
Eldar-Translate/
├── js/                          # Core JavaScript files
│   ├── semantic-translation-engine.js    # Main translation engine
│   ├── advanced-features.js             # Advanced linguistic features
│   ├── tengwar-translator.js            # Tengwar script system
│   └── app.js                          # Main application logic
├── data/                        # Vocabulary and linguistic data
│   ├── english-to-quenya-translation.json
│   ├── english-to-sindarin-translation.json
│   ├── semantic-domains.json
│   └── [other vocabulary files]
├── tests/                       # Test suite and validation
│   ├── comprehensive-test-suite.js
│   └── [test files]
├── css/                         # Styling and fonts
├── fonts/                       # Tengwar font files
└── docs/                        # Documentation
```

### **Development Workflow**

1. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make your changes**
   - Follow the coding standards below
   - Add tests for new functionality
   - Update documentation as needed

3. **Test your changes**
   ```bash
   # Run the comprehensive test suite
   # Ensure all tests pass
   # Check for performance regressions
   ```

4. **Submit a pull request**
   - Provide clear description of changes
   - Include test results
   - Reference related issues

## 📝 **Coding Standards**

### **JavaScript Standards**

- **ES6+ syntax** preferred
- **Consistent indentation** (2 spaces)
- **Descriptive variable names**
- **JSDoc comments** for functions
- **Error handling** for all async operations

### **Code Organization**

```javascript
// Example structure for new features
class NewFeature {
    constructor(engine) {
        this.engine = engine;
        this.initialized = false;
    }

    /**
     * Initialize the feature
     * @param {Object} options - Configuration options
     * @returns {Promise<boolean>} Success status
     */
    async initialize(options = {}) {
        try {
            // Implementation
            this.initialized = true;
            return true;
        } catch (error) {
            console.error('Feature initialization failed:', error);
            return false;
        }
    }
}
```

### **Naming Conventions**

- **Classes**: PascalCase (`SemanticTranslationEngine`)
- **Functions**: camelCase (`translateText`)
- **Constants**: UPPER_SNAKE_CASE (`MAX_VOCABULARY_SIZE`)
- **Files**: kebab-case (`semantic-translation-engine.js`)

## 📚 **Linguistic Data Contributions**

### **Vocabulary Entry Format**

```json
{
    "english": "tree",
    "quenya": {
        "primary": "alda",
        "alternatives": ["ornë", "tál"],
        "source": "LotR",
        "priority": 100,
        "part_of_speech": "noun",
        "semantic_domain": "natural_world",
        "notes": "Common word for 'tree' in Quenya"
    },
    "sindarin": {
        "primary": "galadh",
        "alternatives": ["orn"],
        "source": "LotR",
        "priority": 100,
        "part_of_speech": "noun",
        "semantic_domain": "natural_world",
        "notes": "Standard Sindarin word for 'tree'"
    }
}
```

### **Source Attribution Guidelines**

- **Primary sources**: LotR, Silmarillion, Letters
- **Secondary sources**: VT, PE, scholarly works
- **Community sources**: Well-established linguistic resources
- **Always include**: Author, publication, page/chapter reference

### **Priority System**

- **100**: Directly attested in primary Tolkien sources
- **95-98**: Well-supported scholarly reconstruction
- **85-90**: Pattern-based reconstruction with reasonable evidence
- **70-80**: Specialized terms with limited attestation

## 🧪 **Testing Guidelines**

### **Test Categories**

1. **Unit Tests**: Individual function testing
2. **Integration Tests**: Component interaction testing
3. **Accuracy Tests**: Translation quality validation
4. **Performance Tests**: Speed and memory benchmarks
5. **Source Tests**: Tolkien source verification

### **Test Structure**

```javascript
// Example test structure
describe('Translation Engine', () => {
    let engine;

    beforeEach(async () => {
        engine = new SemanticTranslationEngine();
        await engine.initialize();
    });

    describe('Basic Translation', () => {
        it('should translate simple words correctly', async () => {
            const result = await engine.translate('tree', 'quenya');
            expect(result).toContain('alda');
        });

        it('should handle unknown words gracefully', async () => {
            const result = await engine.translate('xyz123', 'quenya');
            expect(result).toBeDefined();
        });
    });
});
```

### **Running Tests**

```bash
# Open test suite in browser
open tests/comprehensive-test-suite.js

# Or run via Node.js (if available)
node tests/comprehensive-test-suite.js
```

## 🔄 **Pull Request Process**

### **Before Submitting**

1. **Ensure tests pass**
   - All existing tests should pass
   - Add tests for new functionality
   - Check for performance regressions

2. **Update documentation**
   - Update README if needed
   - Add JSDoc comments
   - Update API documentation

3. **Check code quality**
   - Follow coding standards
   - Remove debug code
   - Ensure proper error handling

### **Pull Request Template**

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Linguistic data addition
- [ ] Performance improvement
- [ ] Test addition

## Testing
- [ ] All existing tests pass
- [ ] New tests added for functionality
- [ ] Performance tested
- [ ] Manual testing completed

## Checklist
- [ ] Code follows project standards
- [ ] Documentation updated
- [ ] No breaking changes (or documented)
- [ ] Linguistic data properly attributed
```

## 🐛 **Issue Reporting**

### **Bug Reports**

When reporting bugs, please include:

- **Clear description** of the problem
- **Steps to reproduce** the issue
- **Expected vs actual behavior**
- **Environment details** (browser, OS, etc.)
- **Error messages** or console output
- **Sample input** that causes the issue

### **Feature Requests**

For feature requests, include:

- **Clear description** of the desired feature
- **Use case** and motivation
- **Proposed implementation** (if applicable)
- **Priority level** and impact
- **Related issues** or discussions

### **Issue Templates**

Use the provided issue templates for:
- Bug reports
- Feature requests
- Linguistic data contributions
- Documentation improvements

## 🤝 **Community Guidelines**

### **Communication**

- **Be respectful** and constructive
- **Ask questions** when unsure
- **Share knowledge** and resources
- **Provide context** for suggestions

### **Collaboration**

- **Review others' work** constructively
- **Help newcomers** get started
- **Share linguistic resources** and sources
- **Maintain academic integrity**

### **Quality Standards**

- **Verify sources** before contributing data
- **Test thoroughly** before submitting
- **Document changes** clearly
- **Follow established patterns**

## 📞 **Getting Help**

### **Resources**

- **Project Documentation**: Check README and docs/
- **Test Suite**: Run tests/comprehensive-test-suite.js
- **Issues**: Search existing issues for similar problems
- **Discussions**: Use GitHub Discussions for questions

### **Contact**

- **Issues**: Use GitHub Issues for bugs and features
- **Discussions**: Use GitHub Discussions for questions
- **Security**: Use GitHub Security tab for vulnerabilities

## 🏆 **Recognition**

Contributors will be recognized in:

- **README.md** contributor list
- **CHANGELOG.md** for significant contributions
- **GitHub contributors** page
- **Release notes** for major versions

---

**Thank you for contributing to Eldar-Translate!** Your work helps advance the scholarly study of Tolkien's languages. 