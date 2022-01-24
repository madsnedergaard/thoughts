---
description: 'Best practices, handy tools and snippets, etc.'
---

# Testing JavaScript

## Best Practices

_The following best practices are very inspired by_ [_Yoni Goldberg's ideas_](https://github.com/goldbergyoni/javascript-testing-best-practices)

### Design for lean testing

* Keep tests as simple as possible!
* Avoid "smart" abstractions - DRY is not the goal here

It's better to have 90% coverage in simple, easy-to-read tests than to have 100% coverage with tests that takes a lot of mental effort to understand.

[Great example of anti-pattern in the example here!](https://github.com/goldbergyoni/javascript-testing-best-practices#-%EF%B8%8F13-describe-expectations-in-a-product-language-use-bdd-style-assertions)

### AAA pattern

* Separate the three parts: Arrange, Act, Assert

```javascript
it("works", () => {
  //Arrange
  fetchMock.get(URL, { resources: [] });
  const requestLogin = jest.fn();

  //Act
  const result = myFunction(requestLogin);

  //Assert
  expect(fetchMock).toHaveFetchedTimes(1);
  expect(result).toBe('success');
});


```



### Only test public methods \(black-box\)

* Unless it helps you write the code, don't test internal methods
* It's rarely worth the effort and they are often covered by usage of the external method
* black-box testing **&gt;** white-box testing



### Test the unexpected

* We have a tendency to test for what we're expecting, but the real world operates differently!
* Test with invalid, unexpected or random data and inputs \(also called "[fuzzing](https://en.wikipedia.org/wiki/Fuzzing)"\)
* Consider using [fast-check](https://github.com/dubzzz/fast-check) to do "property-based testing
  * given`myFunc(a: string, b: number, c:boolean)` it will test all possible combinations with random inputs matching types

### Nesting categories is good 👍

* Use multiple `describe()` levels if there are many tests
* Makes it much easier to scan through the output results and to find out what's going on

```javascript
// Unit under test
describe("My Fancy Service", () => {
  //Scenario
  describe("When no credit", () => {
    //Expectation
    it("declines the purchase", () => {});

    //Expectation
    it("notifies user", () => {});
  });
  describe("When credit", () => {
    // ...
  });
});
```

### Focus on low-level tests

* It's better to have a lot of small, low-level unit tests than few, massive tests

> I always argue that high-level tests are there as a second line of test defense. If you get a failure in a high level test, not just do you have a bug in your functional code, you also have a missing or incorrect unit test. – Martin Fowler

![https://martinfowler.com/bliki/TestPyramid.html](../../.gitbook/assets/test-pyramid.png)


## How to ...

### Test multiple cases

Either loop over things, or use [jest-in-case](https://github.com/atlassian/jest-in-case). 
Can be combined with snapshots like this:

```javascript
import cases from 'jest-in-case';
import { sayHi } from './sayHi';

cases(
  'title (e.g. function name)',
  ({ output, snapshot = false }) => {
    if (snapshot) {
      expect(sayHi(output)).toMatchSnapshot();
    } else {
      expect(sayHi(output)).toBe(`Hi ${output}!`);
    }
  },
  {
    'test string': { output: 'John', snapshot: true },
    'test int': { output: 0 },
    'test null': { output: null },
  }
);
```



### Mock express routes

```javascript
// Util for mocking req (that always has a query and headers
// but everything can be overwritten
const mockRequest = (options) => ({ 
  query: {}, 
  headers: {}, 
  ...options 
});

// Util for mocking res
const mockResponse = (options) => {
  const res = {...options};
  res.status = jest.fn().mockReturnValue(res);
  res.json = jest.fn().mockReturnValue(res);
  res.send = jest.fn().mockReturnValue(res);
  return res;
};

// Util for mocking next
const mockNext = () => jest.fn();

// Combining all three into one to make usage easier
const mockExpress = (options) => ({
  req: mockRequest(options.req),
  res: mockResponse(options.res),
  next: mockNext(),
});

it('tests myEndpoint', async () => {
  const { req, res } = mockExpress({ req: { body: { name: 'test' } } });

  await myEndpoint(req, res);

  expect(res.status).toHaveBeenCalledWith(200);
  expect(res.json).toHaveBeenCalledWith({
    message: 'Success',
  });
});
```

## Links

- https://github.com/goldbergyoni/javascript-testing-best-practices

- Util for running "property based testing" - all combos of fun(a: str, b: int, c: bool): https://github.com/dubzzz/fast-check


