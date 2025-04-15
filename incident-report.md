
# Python: Automated Incident Report Generator

**Objective**: Create a Python script to generate a Markdown report from JSON incident data.

**Difficulty**: 7/9  
**Time**: 30 minutes

## Steps

1. **Setup**  
   - Import the required library:  
     ```python
     import json
     ```

2. **Load Data**  
   - Read the incident data from a JSON file:  
     ```python
     with open('incident.json') as f:
         data = json.load(f)
     ```

3. **Format**  
   - Create a Markdown-formatted report string using the JSON data:  
     ```python
     report = f'# Incident Report\nTime: {data["time"]}\nIP: {data["ip"]}\nAction: {data["action"]}'
     ```

4. **Write**  
   - Write the formatted report to a Markdown file:  
     ```python
     with open('report.md', 'w') as f:
         f.write(report)
     ```

5. **Test**  
   - Run the script with a sample `incident.json` file to verify the output in `report.md`.

## Solution

The script generates a Markdown file (`report.md`) containing incident details, such as time, IP, and action, extracted from the provided JSON data.
