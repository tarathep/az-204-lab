# Create a long-running serverless workflow with Durable Functions


## Knownledage Check

```Question 1```

What are the benefits of using Durable Functions in your application?

Select all options that apply.


- You can chain functions together.
  - You can implement common patterns such as fan-out/fan-in, which uses one function to invoke others in parallel, and then accumulate the results.
- The state is managed for you. 
  - You don't have to write your own code to save state information for a long-running function.
- They enable you to write event-driven code.
  - A durable function can wait asynchronously for one or more external events, and then perform a series of tasks in response to these events.
- You can orchestrate and coordinate functions.
  - You can do that, and specify the order in which functions should execute.


```Question 2```

True or False?

Durable functions can be called synchronously, but not asynchronously.
- False
  - Functions can be called both synchronously and asynchronously. 


```Question 3```

Which types of durable functions are available for use?

Select all options that apply.

- Orchestrator
  - These functions describe how actions are executed, and the order in which they are run. You write the orchestration logic in code (C# or JavaScript).
- Client
  - Client functions are the entry point for creating an instance of a Durable Functions orchestration. They can run in response to an event from many sources. You can write them in any of the supported languages.
- Activity
  - These functions are the basic units of work in a durable function orchestration. An activity function contains the actual work performed by the tasks being orchestrated.


```Question 4```

In this pattern, the workflow executes a sequence of functions in a specified order. The output of one function is applied to the input of the next function in the sequence. The output of the final function is used to generate a result. Which application pattern is presented above?
- Function chaining

```Question 5```

Select two capabilities of Azure Durable Functions that differentiate it from Logic Apps.
- Code-first (imperative)
  - With Azure Durable Functions, you develop orchestrations by writing code and using the Durable Functions extension.
- Built-in binding types
  - About a dozen built-in binding types. You can write code for custom bindings.
  