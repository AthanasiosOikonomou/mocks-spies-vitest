# Mock and Spies Vitest

This project demonstrates the use of mocks and spies in unit testing using Vitest. The focus is on testing JavaScript modules and functions with mock implementations and spying on function calls. The project includes several JavaScript files with corresponding test files.

## Project Structure

The project is organized as follows:

### File Descriptions

- **app.js**: Entry point for the application.
- **index.html**: HTML file to serve the application.
- **package.json & package-lock.json**: Project dependencies and scripts.
- **posts/**: Contains post-related modules and test files.
  - **posts.js**: Module for post operations.
  - **posts.test.js**: Unit tests for `posts.js`.
- **util/**: Utility modules and test files.
  - **dom.js**: Utility functions for DOM manipulation.
  - **dom.test.js**: Unit tests for `dom.js`.
  - **errors.js**: Utility functions for error handling.
  - **errors.test.js**: Unit tests for `errors.js`.
  - **http.js**: Utility functions for HTTP requests.
  - **http.test.js**: Unit tests for `http.js`.
  - **validation.js**: Utility functions for validation.
  - **validation.test.js**: Unit tests for `validation.js`.

## .test.js Files

### posts.test.js

This file contains unit tests for the `posts.js` module. The tests cover various post operations and use mocks to simulate API responses.

Example:

```javascript
import { describe, it, expect, vi } from "vitest";
import { fetchPosts } from "./posts";
import * as http from "../util/http";

vi.mock("../util/http");

describe("posts.js tests", () => {
  it("should fetch posts", async () => {
    http.get.mockResolvedValue([{ id: 1, title: "Test Post" }]);

    const posts = await fetchPosts();

    expect(posts).toEqual([{ id: 1, title: "Test Post" }]);
  });
});
```

### dom.test.js

This file includes unit tests for the dom.js module, focusing on DOM manipulation functions and using spies to verify function calls.

Example:

```javascript
import { describe, it, expect, vi } from "vitest";
import { updateElementText } from "./dom";

describe("dom.js tests", () => {
  it("should update element text", () => {
    const element = { innerText: "" };
    const spy = vi.spyOn(element, "innerText", "set");

    updateElementText(element, "New Text");

    expect(spy).toHaveBeenCalledWith("New Text");
  });
});
```

### errors.test.js

This file provides unit tests for the errors.js module, verifying error handling functions and using mocks to simulate different scenarios.

Example:

```javascript
import { describe, it, expect } from "vitest";
import { handleError } from "./errors";

describe("errors.js tests", () => {
  it("should handle error correctly", () => {
    const error = new Error("Test Error");

    const result = handleError(error);

    expect(result).toBe("An error occurred: Test Error");
  });
});
```

### http.test.js

This file includes unit tests for the http.js module, focusing on HTTP request functions and using mocks to simulate network responses.

Example:

```javascript
import { describe, it, expect, vi } from "vitest";
import { get } from "./http";

vi.mock("./http");

describe("http.js tests", () => {
  it("should get data from API", async () => {
    vi.mocked(get).mockResolvedValue({ data: "Test Data" });

    const data = await get("https://api.example.com/data");

    expect(data).toEqual({ data: "Test Data" });
  });
});
```

### validation.test.js

This file provides unit tests for the validation.js module, verifying various validation functions to ensure they operate correctly.

Example:

```javascript
import { describe, it, expect } from "vitest";
import { isValidEmail, isValidPassword } from "./validation";

describe("validation.js tests", () => {
  it("should validate email addresses correctly", () => {
    expect(isValidEmail("test@example.com")).toBe(true);
    expect(isValidEmail("invalid-email")).toBe(false);
  });

  it("should validate passwords correctly", () => {
    expect(isValidPassword("StrongPass1!")).toBe(true);
    expect(isValidPassword("weak")).toBe(false);
  });
});
```

## Running the Tests

To run the tests, follow these steps:

Install dependencies:

```bash
npm install
```

Run the tests:

```bash
npm test
```

The test results will be displayed in the terminal, showing which tests passed and which failed.

## Credits

Special thanks to Maximilian Schwarzmüller and his udemy courses.
