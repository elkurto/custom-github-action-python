# custom-github-action-node
- This repo provides an example of a custom-github-action
- This example is based on udacity Cloud Devops Engineer course - https://youtu.be/iiUdQo5vB6U
- Usage:
  ```yaml
  steps:
    - name: Run custom action
      uses: elkurto/custom-github-action-python@main


  ```
- Files
```yaml
# file = action.yml 
# This file hooks into github actions, and 
# specifed how the github-action-runner should
# execute ./index.js (which contains custom logic)
#
name: 'Business Greetings'
description: 'Offers professional greetings and timestamps them'
inputs:
  name:
    description: 'Name of the person or team to greet'
    required: true
    default: 'Udacity Learner'
outputs:
  timestamp:
    description: 'Time of greeting'
runs:
  using: 'node18'
  main: 'index.js'

```

```yaml
# file = main.py
# custom logic that the github-action-runner executes.
# This custom-github-action just performs 3 activities;
# - reads an optional input parameter, name,
# - logs a silly greeting, and 
# - sets a custom output variable, timestamp. 

import os
from datetime import datetime

def main():
  name = os.getenv('INPUT_NAME', 'Udacity Learner')

  print(f'Hello, {name}! Welcome to Continuous Integration.')
  timestamp = datetime.now().isoformat()
  print(f'Welcome logged at: {timestamp}')
  print(f'::set-output name=timestamp::{timestamp}')

if __name__ == '__main__':
  main()
```
