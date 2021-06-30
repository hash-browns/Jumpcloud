Automation is written for Jmeter

1. Download Jmeter 
http://jmeter.apache.org/download_jmeter.cgi

2. Clone Jumpcloud Repo
3. Move jmeter-jumpcloud.jmx in to apache-jmeter-5.4.1 /bin
4. Run ./jmeter.sh in /bin
5. Open jmeter-jumpcloud.jmx
6. Test plan contains 6 suites
    1. Endpoint tests -  contain assertions on individual endpoints.There are asserions on the json structure of /stats and an assertion that shutdown returns  a 200 response.
    2. End to end - contain no assertions. Assertions can be expensive in Jmeter so the intention was to make this fast
    3. Multiple Theads - Test is configured to run 10 threads and see how the application performs under a more realistic scenario
    4. Use job identifier before hash is computed - This will post to /hash and run a GET on the job id before the 5 seconds needed to calculate the hash
    5. Gracefully shutdown - This will POST to /hash and immediately initate a shutdown but verifies a job id is returned from the first request. 
    6. Shutdown without additional requests - This initiates a shutdown and verifies the GET /hash request will fail.
