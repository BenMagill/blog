+++
date = '2024-11-03T11:52:27Z'
draft = true
title = 'The state of testing in Rust'
+++

What does cargo test do ?
- Building the binaries for testing 
- Running each of them 


Directly using the test binaries
- Cargo test no run option 
- What can you do with the binaries (running specific tests, getting the tests inside of each)

How does the build for testing work?
- The test proc macro 
- Libtest 
- Inserting a new main function, providing the cli that is used 

Customising it 
- Creating a custom test main function
- Custom harness 

Nextest vs cargo test 
- The differences 
- How nextest runs tests differently 

