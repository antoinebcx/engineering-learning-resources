# Types

## Definition

Types are labels that specify the kind of data a variable can hold or a function can accept and return, such as integers, strings, or custom objects.

They are important because they help catch errors early, improve code readability, and enable better tooling support like autocompletion and refactoring.

## Example in code

Python uses dynamic typing at runtime but supports optional type hints for improved code clarity and tool assistance.

```python
from typing import List, Dict

def process_user_data(users: List[Dict[str, str]]) -> Dict[str, int]:
    age_groups: Dict[str, int] = {"0-18": 0, "19-30": 0, "31-50": 0, "51+": 0}
    
    for user in users:
        age = int(user["age"])
        if age <= 18:
            age_groups["0-18"] += 1
        elif age <= 30:
            age_groups["19-30"] += 1
        elif age <= 50:
            age_groups["31-50"] += 1
        else:
            age_groups["51+"] += 1
    
    return age_groups

# Example usage
users_data = [
    {"name": "Alice", "age": "25"},
    {"name": "Bob", "age": "42"},
    {"name": "Charlie", "age": "17"}
]

result = process_user_data(users_data)
print(result)
```

TypeScript enforces types at compile-time through static typing.

```ts
interface User {
    name: string;
    age: string;
}

interface AgeGroups {
    "0-18": number;
    "19-30": number;
    "31-50": number;
    "51+": number;
}

function processUserData(users: User[]): AgeGroups {
    const ageGroups: AgeGroups = { "0-18": 0, "19-30": 0, "31-50": 0, "51+": 0 };
    
    for (const user of users) {
        const age = parseInt(user.age);
        if (age <= 18) {
            ageGroups["0-18"]++;
        } else if (age <= 30) {
            ageGroups["19-30"]++;
        } else if (age <= 50) {
            ageGroups["31-50"]++;
        } else {
            ageGroups["51+"]++;
        }
    }
    
    return ageGroups;
}

// Example usage
const usersData: User[] = [
    { name: "Alice", age: "25" },
    { name: "Bob", age: "42" },
    { name: "Charlie", age: "17" }
];

const result = processUserData(usersData);
console.log(result);
```
