# Pattern Matching and Structured Log Analysis

<h2>Description</h2>
In this Log Analysis task, I used apttern matching queries to filter within an access.log file and json queries to filer within a json file. 


<h2>Languages and Utilities Used</h2>

- <b>linux CLI</b>

<h2>Environments Used </h2>

- <b>Unbuntu</b> 

<br />
<br />
Grepping for error cod "404: within the access.log and appending -n will show the line number of each error code. This is usefull for referencing log lines within an investigation. 

![1) grep, -c, -n for line number](https://github.com/user-attachments/assets/cee30b1d-279d-47f9-8ec0-16074e058aa0)

<br />
<br />
Using "grep -E '%3C|%3E|<|>' access.log" to search for specific encoded and unencoded special characters in the access.log file. -E option enables extended regular expressions, allowing for more complex pattern matching. '%3C|%3E|<|>': This is the search pattern, which looks for:
%3C: URL-encoded representation of <
%3E: URL-encoded representation of >
<: The literal less-than symbol
>: The literal greater-than symbol.

![2) -E to match regular expressions](https://github.com/user-attachments/assets/71dfb264-77c7-41c7-b876-aa4b402254ad)

<br />
<br />  
Using "grep -E '\.\./|%2E%2E%2F|%2E%2E%2E%2E%2F%2F' access.log" to search for potential directory traversal attacks in the access.log file. The search pattern:
\.\.\/: Matches "../" (dot-dot-slash)
%2E%2E%2F: Matches the URL-encoded version of "../"
%2E%2E%2E%2E%2F%2F: Matches a double-encoded version of "../../". 

![3) ](https://github.com/user-attachments/assets/845c1688-0a0c-4e58-ac32-813d4c490739)

<br />
<br />
The command "jq . events.json" is used to parse and display the contents of the JSON file named "events.json" in a formatted and readable manner. Here's what this command does:
jq: This is the command-line JSON processor tool.
. : This is the identity filter, which passes the entire JSON input unchanged to the output.
events.json: This is the name of the JSON file being processed.

![4) JSON](https://github.com/user-attachments/assets/30278a22-a854-452a-9b9f-96e95646e95e)

<br />
<br />
The command jq 'map(.event)' events.json applies the map function to the contents of the events.json file. Here's what it does:
It reads the JSON data from the events.json file.
The map function iterates over each element in the top-level array of the JSON data.
For each element, it extracts the value associated with the "event" key.
The result is a new array containing only the "event" values from each object in the original JSON.
This command is useful for:
Extracting a specific field from a collection of JSON objects.
Simplifying complex JSON structures by focusing on a particular attribute.
Creating a list of event names or types for further analysis or processing.

![5) jq map event](https://github.com/user-attachments/assets/58914678-227e-424a-b3c4-afe02ea2a0c6)
c
<br />
<br />
Using "jq '.[] | select(.event.PROCESS_ID == 3532)' events.json" to filter and extract specific data from the events.json file. Here's what this command does:
.[]: to iterate over all elements in the top-level array of the JSON file.
select(.event.PROCESS_ID == 3532): This selects only the objects where the PROCESS_ID field within the event object is equal to 3532.
events.json: This is the input JSON file being processed.

![6) filter for pid3532](https://github.com/user-attachments/assets/6fb32968-ff0a-493d-9527-9b597c0a5ede)

<br />
<br />
Changing the .event type to file path, hash, or process_id will result in their respective searches. 

![7) extracting certian lines](https://github.com/user-attachments/assets/668a187b-7838-4857-a951-0540891107cd)

<br />
<br />  
Similarly appending .parent will dive deeper into the serach query within the parent.process_id, etc. 

![8) parent extraction](https://github.com/user-attachments/assets/ef8ede5a-422f-409f-aa84-78256f74b379)

<br />
<br />
Here is the script within the exercise to parse json data. 

![9) json script](https://github.com/user-attachments/assets/5f2d97ee-74a1-44cf-b68c-7ca3f6cbcf40)

<br />
<br />
Running the script extracts key details from the json file. 

![10) script to parse info](https://github.com/user-attachments/assets/b2ca81fb-2efd-4fea-9307-1af02728292e)
<br />
<br />  
