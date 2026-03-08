# This is my first Function App

## Prerequisites (once per machine)

#### Azure CLI
`az version`
#### Azure Functions Core Tools v4
`func --version`
##### Python (match Azure runtime)
`python --version   # 3.9 / 3.10 / 3.11 recommended`

## Step 1: Create a local project
`mkdir myfuncapp`

`cd myfuncapp`

`func init . --python`

This creates
`host.json`
`local.settings.json`
`requirements.txt`

## Step 2: Create a local python environment

`python -m venv .venv`

`# Windows`

`.venv\Scripts\activate`

`# Linux / macOS`

`source .venv/bin/activate`

## Step 3: Add a function

`func new`

Example:

Template: HTTP trigger
Function name: HttpExample
Auth level: anonymous

## Step 4: Install Dependencies

`
pip install requests
pip freeze > requirements.txt
`


