Models:
	Language Models
Prompts:
	Style/syntax of taking inputs to models
Parser:
	Take output of models and parsing into structured ones for downstair systems.

	pip install openapi

```python
	get_completion(prompt,model="gpt-3.5-turbo"):
		messages = [{"role":"user","content":prompt}]
		response = openapi.ChatCompletion.create(
			model=model,
			messages=messges,
			temperature=0)
		return response.choices[0].message["content"]
 ```