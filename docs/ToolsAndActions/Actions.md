# Actions Functionality

## Introduction to Actions

Actions within our framework are sequences of one or more tools that are executed in a specific order to perform complex tasks. They offer the capability to combine the functionality of individual tools into cohesive workflows. Actions are flexible and can consist of a single tool or multiple tools, each contributing a step towards the overall objective of the action.

Actions are also defined in YAML files and managed within the `actions` directory in the project, facilitating organized development and straightforward access.

**Actions Directory**: You can find the action definitions in the `your_project_root/.agentforge/actions` directory.

## Defining Actions in YAML

Each action is defined in a YAML file, which includes attributes that detail the steps involved:

- **Name**: The title of the action.
- **Description**: What the action does, explained clearly.
- **Example**: An example command showing how the action could be executed.
- **Instruction**: Step-by-step instructions on how the action should be carried out.
- **Tools**: A list of tools used in the action.

Here's an example of a single-tool action and a multi-tool action defined in YAML format:

### Single Tool Action
```yaml
Name: Write File
Description: >-
  Utilizes the 'File Writer' tool to write or append text to a specified file in a given directory.
Example: >-
  response = write_file('path/to/folder', 'filename.txt', 'This is the content', mode='a')
Instruction: >-
  Specify the target folder, filename, and content to write. Optionally, provide a mode ('a' for append, 'w' for overwrite).
Tools: File Writer
```

### Multi Tool Action
```yaml
Name: Web Search
Description: >-
  Performs a Google search from a query, scrapes text from a returned URL, and breaks the text into chunks.
Example: >-
  search_results = google.google_search(query, number_result);
  url = search_results[2][0];
  scrapped = web_scrape.get_plain_text(url)
Instruction: >-
  Use 'Google Search' to get search results, pick a URL, then 'Web Scrape' to scrape text from the URL.
Tools: 
  - Google Search
  - Web Scrape
```

## Executing Actions

The `ActionExecution` module in our framework takes an action, runs each tool listed in the `Tools` attribute in sequence, and smartly feeds the result from one tool into the next. This allows for a seamless chain of operations, automating complex procedures with ease.

For those interested in the underlying implementation, 
the [ActionExecution](../Modules/ActionExecution.md) module is central to action orchestration.
It's located at `agentforge/modules/ActionExecution.py` within the library package.



### Action Execution Process

1. **Loading Tools**: The action's tools are loaded and prepared for execution.
2. **Running Tools in Sequence**: Each tool is executed in the order specified, with outputs from one tool being used as inputs for the next where necessary.
3. **Handling Results**: The results are collected and can be used for further processing or saved for future reference.

## Example Action Execution Code

The following example demonstrates a generic use case of executing an action within our framework. This example shows how an action can be selected, defined, and then executed using the `Action` class from the `ActionExecution` module.

### Usage Example:

```python
from agentforge.modules.ActionExecution import Action

# Example objective and task for context
objective = "Perform a specific task using a combination of tools."
task = "Describe the specific steps involved in achieving the task."

# Define an action
selected_action = {
  "Name": "Example Action",
  "Description": "This action demonstrates how multiple tools can be combined to perform a complex task.",
  "Example": "result = tool1.method(param1); output = tool2.method(result)",
  "Instruction": "First, execute 'Tool 1' with the specified parameters. Then, use the output from 'Tool 1' as input for 'Tool 2'.",
  "Tools": "Tool 1, Tool 2"
}

class ActionExecutor:

    def __init__(self):
        self.action = Action()

    def execute(self):
        # Additional context for the action
        self.action.data = {'objective': objective, 'task': task}
        # Execute the action and get the result
        result = self.action.run(selected_action)
        return result

if __name__ == '__main__':
    executor = ActionExecutor()
    execution_result = executor.execute()
    print("Execution Result:", execution_result)
```

### Note on Action Attributes:
Not all attributes in the action's YAML file are directly used in execution. While `Name`, `Description`, `Example`, and `Instruction` give context and define the workflow, the `Tools` attribute is crucial as it lists the actual tools to be executed. The `ActionExecution` module is capable of using these definitions to prime and execute each tool, thus completing the action.

## Future Implementations

Our vision includes the development of an 'Action Creation Agent' that can autonomously test different tools together, creating new actions without human intervention. This will significantly expand the capabilities of our system, allowing it to evolve and adapt to new tasks over time.

## Best Practices for Action Definitions

- **Validate Your Actions**: Ensure each action is thoroughly tested to function as intended.
- **Clear Definitions**: Maintain clarity in your YAML definitions to prevent misunderstandings during execution.

By carefully defining your actions in YAML files and understanding how they are executed, you can leverage the full potential of the Action functionality to automate complex tasks within your system.