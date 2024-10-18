# Inheritance

## Definition

Inheritance is a mechanism that allows a new class to be based on an existing class, inheriting its properties and methods.

It's important because it promotes code reuse, enables polymorphism, and helps create hierarchical relationships between classes.

Inheritance should be used when there's a clear "is-a" relationship between classes and shared behavior can be abstracted to a parent class; however, it should be avoided when it leads to deep, complex hierarchies or when composition would provide a more flexible and maintainable solution.

## Example in code

Python:
```python
class DataAnalyzer:
    def __init__(self, data):
        self.data = data

    def analyze(self):
        return f"Analyzing {len(self.data)} data points"

class TextAnalyzer(DataAnalyzer):
    def analyze(self):
        base_analysis = super().analyze()
        word_count = sum(len(text.split()) for text in self.data)
        return f"{base_analysis}\nTotal word count: {word_count}"

class NumericAnalyzer(DataAnalyzer):
    def analyze(self):
        base_analysis = super().analyze()
        average = sum(self.data) / len(self.data)
        return f"{base_analysis}\nAverage value: {average:.2f}"

# Usage
text_data = ["Hello world", "Python is great", "Inheritance example"]
text_analyzer = TextAnalyzer(text_data)
print(text_analyzer.analyze())

numeric_data = [1, 2, 3, 4, 5]
numeric_analyzer = NumericAnalyzer(numeric_data)
print(numeric_analyzer.analyze())
```

Typescript:
```ts
class DataAnalyzer<T> {
    protected data: T[];

    constructor(data: T[]) {
        this.data = data;
    }

    analyze(): string {
        return `Analyzing ${this.data.length} data points`;
    }
}

class TextAnalyzer extends DataAnalyzer<string> {
    analyze(): string {
        const baseAnalysis = super.analyze();
        const wordCount = this.data.reduce((count, text) => count + text.split(' ').length, 0);
        return `${baseAnalysis}\nTotal word count: ${wordCount}`;
    }
}

class NumericAnalyzer extends DataAnalyzer<number> {
    analyze(): string {
        const baseAnalysis = super.analyze();
        const average = this.data.reduce((sum, num) => sum + num, 0) / this.data.length;
        return `${baseAnalysis}\nAverage value: ${average.toFixed(2)}`;
    }
}

// Usage
const textData = ["Hello world", "TypeScript is great", "Inheritance example"];
const textAnalyzer = new TextAnalyzer(textData);
console.log(textAnalyzer.analyze());

const numericData = [1, 2, 3, 4, 5];
const numericAnalyzer = new NumericAnalyzer(numericData);
console.log(numericAnalyzer.analyze());
```

In both examples, we have a base DataAnalyzer class that provides a common analyze method. We then create two specialized classes, TextAnalyzer and NumericAnalyzer, which inherit from DataAnalyzer and override the analyze method to provide more specific functionality.

This demonstrates good use of inheritance because:
- There's a clear "is-a" relationship: both text and numeric analyzers are types of data analyzers.
- The base class provides common functionality (counting data points) that is reused in the child classes.
- The child classes extend the base functionality in ways specific to their data types.
- It allows for polymorphism: we can treat both text and numeric analyzers as generic data analyzers when needed.

This approach allows for easy extension (e.g., adding new types of analyzers) while maintaining a consistent interface for all analyzer types.
