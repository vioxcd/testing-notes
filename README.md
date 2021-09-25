# Python Testing Notes

## Notes

### Testing Notes

#### [Red, Green, Refactor](https://youtu.be/B1j6k2j2eJg)

1. Write the tests that met the feature requirements (think about the requirements)
2. **RED**: Run the tests and make sure it fails
3. Write the simplest code so that the test pass (met the specs, clean it up later)
4. **GREEN**: Make all the tests pass (make sure new feature doesn't break other things)
5. **REFACTOR**: improve your code

Testing Tips

- Isolate tests (setup ~ teardown)
- Don't test python STL
- Compare test output with fixed values (and don't just copy implementation from working code to test suites)

#### [Python Testing](https://realpython.com/python-testing/#where-to-write-the-test)

1. Writing your test
   - if it's a single src directory, use test.py on top of or within the src directory tree
   - if it's multiple directory, use a tests directory
   - if it's a single script, use `__import__()`
2. When to write test (question to ask & flow)
   - What do you want to test?
   - Are you writing a unit test or an integration test?
   - Flow: consider the input, execute the process & capture output, compare output to expected result
   - Make sure tests are repeatable and run your test multiple times to make sure it gives the same result every time (seed)
3. Advanced testing scenarios
   - It’s common practice to create **fixtures** and reuse them when your application need certain class or context
   - If you’re running the same test and passing different values each time and expecting the same result, this is known as **parameterization**.
   - There’s a special way to handle expected errors. You can use `.assertRaises()` as a context-manager
   - There are some simple techniques you can use to test parts of your application that have many side effects: refactor following SRP, mocking to remove side effects, use integration tests instead of unit tests
4. Integration testing is the testing of multiple components of the application to check that they work together. Integration testing might require acting like a consumer or user of the application (calling API, webservice, or using the command line). The most significant difference: integration tests are checking more components at once and therefore will have more side effects than a unit test. (also, more fixtures; db connection, socket, config files)
5. A simple way to separate unit and integration tests is simply to put them in different folders (use `discover -s` to select running certain test types)
6. A good way to test data-driven application is to store the test data in a folder within your integration testing folder called fixtures to indicate that it contains test data. Then, within your tests, you can load the data and run the test.
7. [Tox](https://realpython.com/python-testing/#testing-in-multiple-environments): test for multiple environments
8. [Automation of tests execution](https://realpython.com/python-testing/#automating-the-execution-of-your-tests)
9. [Linters](https://realpython.com/python-testing/#introducing-linters-into-your-application): passive (flake8) / aggressive (black)
10. [Performance](https://realpython.com/python-testing/#testing-for-performance-degradation-between-changes): pytest-benchmark
11. [Bandit](https://realpython.com/python-testing/#testing-for-security-flaws-in-your-application): security

#### [Barebones to Functional Automated Test](https://youtu.be/DhUpxWjOhME)

1. Separate your test code from your application code
2. Make your project installable, your test should run no matter where they are (don't depend on (relative ) imports) ([helpful links](https://stackoverflow.com/a/49039535/8996974))
3. Create development requirement file (config for pytest, mypy, flake8, tox, etc.)
4. Write your tests
5. Test on multiple env with tox
6. Always run your pytest after coding, but check with tox first before commit & push
7. Pytest features: assert equal, on raise error, fixtures, mocking/monkeypatch

#### Others

1. [Great intro to unittest](https://youtu.be/6tNS--WetLI):
   - "Test should be [isolated](https://realpython.com/python-testing/#isolating-behaviors-in-your-application): it shouldn't rely on other test or affect other test"
   - [Side effects](https://realpython.com/python-testing/#side-effects) make unit testing harder since, each time a test is run, it might give a different result, or even worse, one test could impact the state of the application and cause another test to fail
   - "Mocking = testing things that are NOT within our control"

2. `python -m unittest discover -s tests` saved me from errors! [yay](https://realpython.com/python-testing/#executing-test-runners) for [this](https://docs.python.org/3/library/unittest.html#test-discovery)
3. [Python CLI testing](https://realpython.com/python-cli-testing/): "Each test treats the method being tested in isolation: outside calls are overridden with a technique called mocking to give reliable return values and any object set up before the test is removed after the test. These techniques and others are done to assure the independence and isolation of the unit under test."
4. Serious Python:
   - Consider your project strucutre, it should be fairly simple. Organize your code based on **features**, not on types
   - Version numbering: PEP 440. (mine would probably be 0.1a, 0.1b, 0.1rc, 0.1dev, 0.1post)
   - Coding style & static analysis: check out [flake8](https://pypi.org/project/flake8/) (you can use tox to automate this)
   - External libraries safefy checks: python3 compatibility, active development, active maintenance, packaged with OS dists., API compatibility, license.
   - `pip --user`: You can also provide a --user option that makes pip install the package in your home directory. This avoids polluting your operating system directories with packages installed system­wide.
   - `pip --editable`: One very valuable feature of pip is its ability to install a package without copying the package’s file. The typical use case for this feature is when you’re actively working on a package and want to avoid the long and boring process of reinstalling it each time you need to test a change.
5. [Tempfile](https://docs.python.org/3/library/tempfile.html): library for creating temporary files