GoogleTest Primer

Tests should be independent and repeatable (lâp lại)
Tests should be well organized(tổ chức tốt) and reflect the structure(phản ánh cấu trúc) of the tested code
Tests should be portable(linh dộng) and reusable(tái sử dụng).
When tests fail, they should provide as much information about the problem as possible.
The testing framework should liberate test writers from housekeeping chores and let them focus on the test content ( dừng bắt đi dọn code, hãy để tui test thôi)
Tests should be fast (này phụ thuộc vào ý đầu, test phải dộc lập).
What is the test cas, test suite
Test suit is grouping related tests,
A test suite contains one or many tests.
Test case: one test case in a test suite
Basic Concepts
assertions: An assertion’s result can be success, nonfatal failure, or fatal failure
If a fatal failure occurs, it aborts the current function; otherwise the program continues normally.
A test suite contains one or many tests.
A test program can contain multiple test suites.
ASSERT_ : stop:
EXPECT_: fail, but continue : EXPECT_TRUE, EXPECT_FALSE, EXPECT_EQ, EXPECT_NE, EXPECT_LT…
https://google.github.io/googletest/reference/assertions.html
Simple Tests
Use the TEST() macro to define and name a test function
--dành cho test fun bình thường thôi, còn test class thì dùng Test_F
naming functions and classes.
Test Fixtures: Using the Same Data Configuration for Multiple Tests
1.	Derive a class from testing::Test . Start its body with protected:, as we’ll want to access fixture members from sub-classes.
2.	Inside the class, declare any objects you plan to use.
3.	If necessary, write a default constructor or SetUp() function to prepare the objects for each test. A common mistake is to spell SetUp() as Setup() with a small u - Use override in C++11 to make sure you spelled it correctly.
4.	If necessary, write a destructor or TearDown() function to release any resources you allocated in SetUp() . To learn when you should use the constructor/destructor and when you should use SetUp()/TearDown(), read the FAQ.
5.	If needed, define subroutines(chương trình con) for your tests to share.
For each test defined with TEST_F(), GoogleTest will create a fresh test fixture at runtime, immediately initialize it via SetUp(), run the test, clean up by calling TearDown(), and then delete the test fixture.
vậy suy ra là 1 Test_F nó đều new sau đó delete, 1 Test_F độc lập chứ ko phải gom nó làm 1 test suite
nó chú ý nè. 
Note that different tests in the same test suite have different test fixture objects, and GoogleTest always deletes a test fixture before it creates the next one. Any changes one test makes to the fixture do not affect other tests.
Invoking the Tests
When invoked, the RUN_ALL_TESTS() macro:
•	Saves the state of all GoogleTest flags.
•	Creates a test fixture object for the first test.
•	Initializes it via SetUp().
•	Runs the test on the fixture object.
•	Cleans up the fixture via TearDown().
•	Deletes the fixture.
•	Restores the state of all GoogleTest flags.
•	Repeats the above steps for the next test, until all tests have run.
If a fatal failure happens the subsequent steps will be skipped.
Writing the main() Function
nhớ return RUN_ALL_TESTS(); là xong
