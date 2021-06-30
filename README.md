# Jumpcloud
| Test Scenario                                                                                 | Result                                                                                                                                                                                               | Why was this tested                                                                                                                                                      |
| --------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Can I accept requests on port 8088 if it’s specified in the the export?                       | Yes                                                                                                                                                                                                  | Part of acceptance criteria                                                                                                                                              |
| Can I accept requests on a different port other than what was set in the export ?             | No                                                                                                                                                                                                   | It could be a potential security issue if a requests can be made to any port                                                                                             |
| Can I accept requests on port 8089 if it’s specified in the the export?                       | Yes                                                                                                                                                                                                  | Curious if port 8088 was hardcoded in the app                                                                                                                            |
|                                                                                               |                                                                                                                                                                                                      |                                                                                                                                                                          |
| POST /hash                                                                                    |                                                                                                                                                                                                      |                                                                                                                                                                          |
| Does a POST to /hash return a job identifier?                                                 | Yes                                                                                                                                                                                                  | Part of acceptance criteria                                                                                                                                              |
| Does a POST to /hash wait 5 seconds before computing a hash?                                  | Yes                                                                                                                                                                                                  | Part of acceptance criteria and might be necessry to know for automating runs that complete in less than 5 seconds                                                       |
|                                                                                               |                                                                                                                                                                                                      |                                                                                                                                                                          |
| GET /hash                                                                                     |                                                                                                                                                                                                      |                                                                                                                                                                          |
| Can I make a GET request to /hash with a job identifier                                       | Yes                                                                                                                                                                                                  | Part of acceptance criteria                                                                                                                                              |
| Can I make a GET request to /hash without a job identifier                                    | Response is GET Not Supported                                                                                                                                                                        | Curious about error handling                                                                                                                                             |
| Can I make a GET request to /hash to a job that doesnt exist                                  | Returns 'Hash not found'                                                                                                                                                                             | Curious about error handling                                                                                                                                             |
| Does a GET to /hash return a hash?                                                            | Yes                                                                                                                                                                                                  | Part of acceptance criteria                                                                                                                                              |
| Does a GET to /hash return a hash in Base64?                                                  | Hash is in base64. Supported characters are A–Z , a–z , 0–9 , + , / and = . String is multiple of 4                                                                                                  | Part of acceptance criteria                                                                                                                                              |
| Is the hash unique to each job identifier?                                                    | Hash is the same for every job. Seems correct since I’am passing the same password input but I expected it to be unique to each corresponding POST request                                           | If the hash corresponds to the a job ID, I thought each job would have a unique hash. Since we are hashing the same data, it seems appropriate that this doesnt change   |
|                                                                                               |                                                                                                                                                                                                      |                                                                                                                                                                          |
| GET /hash                                                                                     |                                                                                                                                                                                                      |                                                                                                                                                                          |
| Can I make a GET request to /stats                                                            | Yes                                                                                                                                                                                                  | Part of acceptance criteria                                                                                                                                              |
| Is the response from /stats in JSON                                                           | Yes                                                                                                                                                                                                  | Part of acceptance criteria                                                                                                                                              |
| Does a GET request to /stats return the total number of hash requests since the server starts | Should /stats count the total number of POST’s to /hash or both POST’s and GET’s to /hash? Currently, /stats only counts the POST’s to create a hash.                                                | Acceptance criteria discusses /stats will calculate the total hash requests. Is this a calculation of requests to create hashes or all requests to /hash?                |
| Does a GET request to /stats return the average time in miliseconds ?                         | No, not sure how this is being computed but I'm seeing the average a lot higher than I would expect. If I make 1 request to /hash it takes about 5 seconds but the average in /stats is ~250 seconds | Part of acceptance criteria. Number seemed high given the speed of the responses.                                                                                        |
| Can I make a GET request to /stats when no hash requests have been made?                      | Yes, just returns 0 TotalRequest and 0 averageTime                                                                                                                                                   | Curious if it would come back null or return an error                                                                                                                    |
|                                                                                               |                                                                                                                                                                                                      |                                                                                                                                                                          |
|                                                                                               |                                                                                                                                                                                                      |                                                                                                                                                                          |
| Can I make a POST request to /hash to shutdown                                                | Yes                                                                                                                                                                                                  | Part of acceptance criteria                                                                                                                                              |
| Can the application accept multiple requests at once?                                         | Yes                                                                                                                                                                                                  | This is a more realistic scenario and useful to stress the application and identify any bottlenecks in performance                                                       |
| Can the application support a graceful shutdown?                                              | Yes                                                                                                                                                                                                  | Bad user experience if we are dropping requests. Applciation should be resilient if it goes down.                                                                        |
| Can additional password requests be made after a shutdown is initiated?                       | Additonal requests can be made after shutdown but I receive an error                                                                                                                                 | request may be lost unless it's being stored until applications is running again. Could be bad user experience if request is lost or doesnt give a helpful error reponse |
|                                                                                               |                                                                                                                                                                                                      |                                                                                                                                                                          |
| Potential Bugs                                                                                |                                                                                                                                                                                                      |                                                                                                                                                                          |
| Hash is the same for every job.                                                               |                                                                                                                                                                                                      |                                                                                                                                                                          |
| Average in /stats doesnt appear to be the correct average                                     |                                                                                                                                                                                                      |                                                                                                                                                                          |
| Should /stats count the total number of POST’s to /hash or both POST’s and GET’s to /hash?    |                                                                                                                                                                                                      |                                                                                                                                                                          |
| Additonal requests can be made after shutdown but I get an error response 
