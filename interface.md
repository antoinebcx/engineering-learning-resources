# Interface

## Definition

An interface is a contract that specifies a set of methods or properties that a class must implement, without defining their implementation details.

It's important because it enables abstraction, promotes loose coupling between components, and facilitates polymorphism.

Interfaces should be used when you want to define a common behavior for multiple classes, especially in scenarios involving dependency injection or when designing pluggable architectures; however, they may be unnecessary for simple, concrete classes with no anticipated variations or when full method implementations are required.

## Example in code

Python:
```python
from abc import ABC, abstractmethod
from typing import List, Dict

class DataProcessor(ABC):
    @abstractmethod
    def read_data(self) -> List[Dict]:
        pass

    @abstractmethod
    def write_data(self, data: List[Dict]) -> None:
        pass

class CSVDataProcessor(DataProcessor):
    def __init__(self, filename: str):
        self.filename = filename

    def read_data(self) -> List[Dict]:
        # Implementation to read from CSV
        pass

    def write_data(self, data: List[Dict]) -> None:
        # Implementation to write to CSV
        pass

class JSONDataProcessor(DataProcessor):
    def __init__(self, filename: str):
        self.filename = filename

    def read_data(self) -> List[Dict]:
        # Implementation to read from JSON
        pass

    def write_data(self, data: List[Dict]) -> None:
        # Implementation to write to JSON
        pass

# Usage
csv_processor = CSVDataProcessor("data.csv")
json_processor = JSONDataProcessor("data.json")

def process_data(processor: DataProcessor):
    data = processor.read_data()
    # Process the data
    processed_data = [item for item in data if some_condition(item)]
    processor.write_data(processed_data)

process_data(csv_processor)
process_data(json_processor)
```

TypeScript:
```ts
interface DataProcessor {
    readData(): Promise<Record<string, any>[]>;
    writeData(data: Record<string, any>[]): Promise<void>;
}

class CSVDataProcessor implements DataProcessor {
    constructor(private filename: string) {}

    async readData(): Promise<Record<string, any>[]> {
        // Implementation to read from CSV
        return [];
    }

    async writeData(data: Record<string, any>[]): Promise<void> {
        // Implementation to write to CSV
    }
}

class JSONDataProcessor implements DataProcessor {
    constructor(private filename: string) {}

    async readData(): Promise<Record<string, any>[]> {
        // Implementation to read from JSON
        return [];
    }

    async writeData(data: Record<string, any>[]): Promise<void> {
        // Implementation to write to JSON
    }
}

// Usage
const csvProcessor = new CSVDataProcessor("data.csv");
const jsonProcessor = new JSONDataProcessor("data.json");

async function processData(processor: DataProcessor) {
    const data = await processor.readData();
    // Process the data
    const processedData = data.filter(item => someCondition(item));
    await processor.writeData(processedData);
}

processData(csvProcessor);
processData(jsonProcessor);
```

In both examples, we define a DataProcessor interface (or abstract base class in Python) that specifies two methods: read_data (or readData in TypeScript) and write_data (or writeData in TypeScript). We then implement this interface for two different data formats: CSV and JSON.

This approach demonstrates good practices because:
- It allows for abstraction: The process_data function can work with any object that implements the DataProcessor interface, without needing to know the specifics of how the data is read or written.
- It promotes loose coupling: We can easily add new data processors (e.g., for XML or database) without changing the existing code.
- It facilitates code reuse and maintainability: Common data processing logic can be shared across different data sources.
- It adheres to the SOLID principles, specifically the Dependency Inversion Principle: High-level modules (like process_data) depend on abstractions (the DataProcessor interface) rather than concrete implementations.

This pattern is particularly useful in scenarios where you need to work with multiple data sources or formats, or when you want to make your code more flexible and extensible for future requirements.
