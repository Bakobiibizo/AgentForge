# Custom Agents

---

## Creating Custom Agents

Creating a Custom Agent is pretty straightforward.
A class only needs to inherit from the base `Agent` class.
By doing so, it gains access to all the default behaviors defined in the `Agent` class.

Creating a Custom Agent from the base class is pretty straightforward. All you need to do is create a new `Python` class that inherits from the base `Agent` class. 

Once that's set up, you have the freedom to override any of the default methods to fit your specific needs. Don't forget to create a corresponding `YAML` file for your agent's prompts; it should be named after your agent class and is case-sensitive. And just like that, you've got yourself a fully customized agent ready to tackle whatever tasks you throw its way!

### Example
```python
from agentforge.agent import Agent

class NewAgent(Agent):
    pass
```

In this example, `NewAgent` will behave exactly like its `Agent` base class since it doesn't override any methods.

---

## Persona Files

Each bot or architecture can have one or more personas,
which are defined by Persona `YAML` files located in the `./agentforge/personas` folder.
The persona file contains all the data related to the persona of the Cognitive Architecture (bot).
For more details on how to structure the `Persona YAML File`,
check out the [Persona Documentation](../Personas/Personas.md).

---

## Agent Prompt Templates

Each custom agent has its own `YAML` file located in the `./agentforge/agents/` folder. This file contains the specific prompt templates used by that agent. The naming convention is crucial here: the filename must match the class name of your agent, and is case-sensitive. So, if you've got a custom agent class named `NewAgent`, your `YAML` file should be `NewAgent.yaml`.

By adhering to this naming convention and populating your `YAML` file with prompt templates, you can create a unique custom agent that inherits default behaviors from the `Agent` base class but also has its own tailored interactions. This approach greatly simplifies and streamlines the agent creation process, making it easier for you to focus on what your agent should do, rather than how it should do it.

For more details on how to structure your agent's prompts, you can refer to the [Agent Prompts Documentation](AgentPrompts.md).

---

## Overriding Agent Methods

If you need to customize the behavior of a custom agent, you can override any of the inherited [Agent Methods](AgentMethods.md). This allows for flexibility in how the agent behaves without affecting the overall architecture.

### Example
```python
class NewAgent(Agent):

    def process_data(self):
        # Custom behavior here
        # ...
     
    
    def save_result(self):
        # Custom behavior here
        # ...
```

In this example, `NewAgent` overrides the `process_data` and `save_result` methods to implement custom behavior. When a method is overridden, the agent's `run` method will automatically call the new version instead of the default one. Want the best of both worlds? You can actually call the default method within your overridden version using the `super()` function. This way, you can extend the default behavior while adding your own special sauce.

---