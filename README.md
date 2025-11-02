# Blog Task - 1

### 1. What are some differences between interfaces and types in TypeScript?
**Understanding Interfaces vs Types in TypeScript**
TypeScript provides two powerful ways to define the shape of data: interfaces and type aliases. While they may seem similar at first glance, they have distinct differences that can impact how you structure your code.

**1. Declaration Merging**
One of the key differences between interfaces and types is that interfaces can take advantage of declaration merging. This means you can define the same interface multiple times, and TypeScript will merge them into a single interface. This is particularly useful for extending existing interfaces or adding new properties.

```ts
interface User {
    id: number;
    name: string;
}

interface User {
    email: string;
}

// Merged interface
const user: User = {
    id: 1,
    name: "John",
    email: "john@example.com"
};
```

On the other hand, type aliases do not support declaration merging. If you try to define a type with the same name multiple times, you will get an error.

```ts
type User = {
    id: number;
    name: string;
};

type User = {
    email: string;
}; // Error: Duplicate identifier 'User'.
```

**2. Extending**
Both interfaces and types can be extended, but they do so in different ways. Interfaces use the `extends` keyword, while types use intersections.

```ts
interface Person {
    id: number;
    name: string;
}

interface Employee extends Person {
    role: string;
}

// Usage
const employee: Employee = {
    id: 1,
    name: "Jane",
    role: "Developer"
};
```

For type aliases, you can achieve a similar effect using intersections:

```ts
type Person = {
    id: number;
    name: string;
};

type Employee = Person & {
    role: string;
};

// Usage
const employee: Employee = {
    id: 1,
    name: "Jane",
    role: "Developer"
};
```

**3. Use Cases**
In general, interfaces are preferred when defining the shape of objects, especially when you expect the shape to evolve over time. They are also the go-to choice when working with classes, as they can be implemented by classes.

Type aliases are more flexible and can represent a wider variety of types, including primitives, unions, and tuples. They are often used for more complex type definitions that go beyond just object shapes.

**Conclusion**
In summary, while interfaces and type aliases in TypeScript can often be used interchangeably, understanding their differences can help you make more informed decisions about how to structure your code. Use interfaces for object shapes and class contracts, and leverage type aliases for more complex type definitions.


# Blog Task - 2

### 7. Provide an example of using **union** and **intersection** types in TypeScript.

**Understanding Union and Intersection Types in TypeScript**
TypeScript offers powerful tools for defining complex types through union and intersection types. These features allow developers to create flexible and reusable type definitions that can enhance code readability and maintainability.

**Union Types**
Union types allow you to define a variable that can hold multiple types. This is useful when a value can be one of several types.

```ts
type StringOrNumber = string | number;

function printId(id: StringOrNumber) {
    console.log("Your ID is: " + id);
}

printId(123);       // Valid
printId("abc");     // Valid
```

**Intersection Types**
Intersection types allow you to combine multiple types into one. This is useful when you want to create a new type that has all the properties of the combined types.

```ts
type Person = {
    name: string;
    age: number;
};

type Employee = Person & {
    employeeId: number;
};

const employee: Employee = {
    name: "Jane",
    age: 30,
    employeeId: 12345
};
console.log(employee);
```
**Combining Union and Intersection Types**
You can also combine union and intersection types to create even more complex type definitions.

```ts
type StringOrNumber = string | number;

type User = {
    id: number;
    name: string;
};

type Admin = User & {
    role: "admin";
};

type Guest = User & {
    role: "guest";
};

type UserRole = Admin | Guest;

function printUserRole(user: UserRole) {
    console.log(`User ${user.name} has role: ${user.role}`);
}
const admin: Admin = { id: 1, name: "Alice", role: "admin" };
const guest: Guest = { id: 2, name: "Bob", role: "
guest" };
printUserRole(admin); // User Alice has role: admin
printUserRole(guest); // User Bob has role: guest
```

**Conclusion**
Union and intersection types in TypeScript provide powerful ways to define flexible and reusable types. By leveraging these features, developers can create more expressive type definitions that enhance code quality and maintainability.

