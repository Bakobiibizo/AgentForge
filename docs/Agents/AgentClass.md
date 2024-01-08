# `Agent` Base Class

---

## Overview
The `Agent` class serves as the **Base Class** for all agents in the framework. It handles core functionalities such as data loading, prompt generation, LLM execution, and more.

### Agent as a Default Template

The `Agent` base class serves as a default template for creating new agents. By providing basic functionalities and methods that can be overridden, it simplifies the process of defining specialized agents. For more details on how to create custom agents by extending this class, refer to the [Custom Agents](CustomAgents.md) page.


---

## Attributes
- `agent_name`: Holds the name of the agent, which defaults to the class name.
- `agent_data`: Contains data specific to the agent, loaded from storage.
- `data`: Placeholder for any data that will be used by the agent, this data may be used in prompt rendering.
- `prompt`: Placeholder for any prompt templates used by the agent.
- `result`: Placeholder for the raw result returned by the Large Language Model (LLM).
- `output`: Placeholder for the final output returned by the agent.
- `storage`: Interface to the data storage component.

---

## Class Initialization

### `__init__(self, log_level='info')`

**Purpose**: Initializes an instance of the `Agent` class. It sets up essential attributes and initializes data storage and logging.

**Arguments**:
- `log_level`: Optional. Specify the logging level. Defaults to `info`.

**Initialization Steps**:
1. Set `agent_name` to the class name.
2. Initialize placeholders for `data`, `prompt`, `result`, `parsed_result`, and `output`.
3. Initialize `Function` Utilities.
4. Load agent data using `self.functions.agent_utils.load_agent_data`.
5. Initialize data storage from `self.agent_data['storage']`.
6. Create a `Logger` instance and set its log level.

```python
def __init__(self, log_level="info"):
    """Initializes the Agent, loads the relevant data depending on it's name and sets up the storage and logger"""
    self.agent_name = self.__class__.__name__
    self.data = None
    self.prompt = None
    self.result = None
    self.output = None

    self.functions = Functions()
    self.agent_data = self.functions.agent_utils.load_agent_data(self.agent_name)
    self.storage = self.agent_data['storage']

    self.logger = Logger(name=self.agent_name)
    self.logger.set_level(log_level)
```

---

## Main Agent Methods

For a detailed walkthrough of the main methods in the `Agent` class that are essential for creating [Custom Agents](CustomAgents.md), please refer to the [Agent Methods](AgentMethods.md) Page.

---