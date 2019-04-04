# TDD

## Legacy Code

### Code that already exists

- The broadest definition
- “If it existed before I got here, it’s legacy”

### Code that you don’t understand\*\*

- Narrowing the definition
- POJO’s, Getters and Setters etc. aren’t hard to deal with.
- But that one business logic class leaves everyone scratching their heads

### Code without tests - Michael Feathers

- A broad, yet narrow, definition.
- Not all legacy code is old.
- Brand new code without tests goes stale, fast.
- Plenty of teams create mountains of fresh legacy code every day.

## Legacy Code - Challenges

Working with Legacy Code can be challenging, writing good tests for Legacy Code is no exception

- It can be hard to even know where to start when you’re looking at code you’ve never seen before.
- In some cases, your code will be tightly coupled to an external system. Be it a DB, Server or other service.
- Your methods and classes may be massive, making them difficult to test.
- Your code may have inumerable, direct, dependencies making it very difficult to isolate just the code you’re looking at.

Later in this deck we’ll talk about some strategies for working with Legacy Code and getting around these challenges.

## What is TDD?

- We all share the common goal of writing clean code, that does what we say it does.
- TDD helps us get there.

## What is TDD?

- The TDD mantra. Red, Green, Refactor!
- Red: write the test you wish you had, infer whatever you like about the API. You’re writing it!
- Green: commit whatever sins you need to to get the test to pass. Remember, they won’t be around very long.
- Refactor: correct your sins, remove duplication, constants and fake implementations

## Benefits Of TDD: Short Term

### For Devs:

- Fast Feedback: We’re writing our own tests, we don’t have to wait for QA to tell us we made a mistake
- Less Debugging: We tested our code as we wrote it, we don’t need to run the app to verify that it works
- Design Improvements: SOLID code, smaller classes/methods

### For QA:

- Lower Defect Density
- QA can spend less time doing low-level bug hunting
- Spend more time proactively testing Performance, Resilience and Usability

### For the Product Owners:

- Fewer nasty surprises: Plan with confidence knowing that new features will perform as expected and be unlikely to cause production issues

## Benefits of TDD: Long Term

### Documents existing behavior:

- Tests can act like living documentation for the code, technical discussions no long require a period of investigation/repparation.
  - Just look at the tests, and reason about how they should change.
- If a user request breaks an existing test, have a conversation about whether that scenario is still valid / important / desirable.

### Reduced cost of change:

- higher certainty in what the code currently does
- higher certainty in what new code does
- means you spend less time with
  - broken builds
  - QA ping-pong
  - dealing with production problems.

### Increased confidence:

- more working software to customers, sooner

### Safety net:

- your existing test cases can verify that a quick fix hasn’t done more damage
- Refactorings and rewrites are much less likely to introduce bugs
- Add functionality without breaking existing use cases

## TDD is not

### Replacement for QA:

- Tests created via TDD aren’t a suitable replacement for QA.
- There are always corner cases, funky user inputs and real life issues that our code needs to be exposed to.

### Upfront:

- TDD doesn’t mean knowing your implementation in advance.
- It means thinking about what interface you’d like, and writing tests to get you there.

### No Plan:

- TDD doesn’t mean you can start building a feature with no thought at all.
- Thinking about how you want to interact with your new code, and what it should do is very important.

### 100% Coverage:

- TDD doesn’t mean every single line of your code will be covered
- Done well it means at least every statement will be covered.

### Expensive:

- What TDD costs in development time, it saves in QA, bug hunting, troubleshooting, build-fixing and nail-biting when deploying.

### Silver bullet:

- TDD is not a silver bullet
- it does not guarantee your software will never break
- it’s not always the best way to approach a new feature (though instances where it’s not are exceedingly rare)
