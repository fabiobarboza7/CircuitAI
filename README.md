![Prancheta 1](https://github.com/user-attachments/assets/c1ccf70b-95ed-4968-b8ee-040590fff276)

A powerful TypeScript library that helps developers efficiently and scalably orchestrate multiple artificial intelligence agents.

#### Join our [Discord](https://discord.gg/ABrXedeeV6) to discuss the project, contribute, ask questions and get updates.

## Concepts

It was inspired by how humans work in teams, where each person has a specific role and responsibility. In CircuitAI, each agent has a goal, context, and rules to follow. The agents can communicate with each other and the supervisor to achieve the project's goal.

### Project

Much like a real-life project, it has a name, description, agents, and a supervisor. The project is responsible for managing the agents and their interactions to achieve a business goal.

### Agent

An agent is a participant in the project. It has a name, goal, context, and rules. The agent can perform actions based on the input it receives and can also communicate with other agents and the supervisor.

### Supervisor

The supervisor is an agent with special privileges. It can oversee other agents, provide guidance, and make decisions based on the agents' actions.

### Task (not ready yet)

A task is a specific action that one or more agents can perform. It can be a simple task like "check credit score" or a complex task like "detect fraud in transactions." Tasks are optional and can be used to chain specific agents and actions together.

## Example

```typescript
import { Project, Agent } from "circuitai";

const managerAgent = new Agent({
  name: "Manager",
  goal: "Supervise other agents",
  context: "You are the manager of the project...",
  action: async ({ content, llmAdapter }) => {
    // Call the LLM
    const response = await llmAdapter?.createText({...});
    // Do something with the response
    return { output: response };
  },
});

const fraudAgent = new Agent({
  name: "FraudAnalysis",
  goal: "Analyze data to detect fraud",
  context: "You have a dataset with transactions...",
  action: async ({ content, llmAdapter }) => {
    // Or instead calling the LLM, do whatever you want here
    // ... and return the output
  },
});

const creditAgent = new Agent({
  name: "CreditAnalysis",
  goal: "Check credit score and limit",
  context: "Your customer is buying a product...",
  rules: "You dont have to check credit score if the transaction ...",
  action: async ({ content, llmAdapter }) => {
    const response = await llmAdapter?.createText({ input: "...." });
    return { output: response };
  },
});

const project = new Project({
  name: "Super Bank",
  description: "Analyzes transactions and checks credit",
  agents: [fraudAgent, creditAgent],
  supervisor: managerAgent,
});
// ...

const response = await project.start({
  input: "Check credit score of the customer 1234",
});

console.log(response);
// {
//   success: true,
//   output: {
//     finalResponse: 'The credit score of the customer is 750',
//     circuits: [
//       {
//         agent: 'CreditAnalysis',
//         input: 'Check credit score of the customer 1234',
//         triagingInput: 'score of customer 1234',
//         output: {....},
//         proccessTime: 12 //ms
//       },
//       {
//         agent: 'FraudAnalysis',
//         input: 'Check credit score of the customer 1234',
//         triagingInput: 'Any restrictions for customer 1234?',
//         output: {....},
//         proccessTime: 4 //ms
//       }
//     ]
//   }
// }
```

## Features

- 🚀 **Scalable**: Easily add new agents to your project
- 🧠 **Contextual**: Agents can have different contexts
- 📚 **Rules**: Define rules for each agent
- 🤖 **LLM Integration**: Use LLMs to generate responses
- 📦 **Extensible**: Create custom adapters for different LLMs
- 📝 **Typescript**: Written in TypeScript

## Contributors

We would like to thank the following people for their contributions:

- **Fabio Souza (@fabio.bcs)** - Project Lead & Software Engineer
- **Bernardo Souza (@bernardoavsouza)** - Software Engineer
- **Caio Rosas (@bycaiodesigner)** - Designer

If you would like to contribute, please join our [Discord](https://discord.gg/ABrXedeeV6) and get in touch!
