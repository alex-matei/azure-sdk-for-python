# Form Recognizer Performance Tests

In order to run the performance tests, the `devtools_testutils` package must be installed. This is done as part of the `dev_requirements` install.
Start by creating a new virtual environment for your perf tests. This will need to be a Python 3 environment, preferably >=3.7.

### Setup for test resources

The following environment variables will need to be set for the tests to access the live resources:

```
FORMRECOGNIZER_TEST_ENDPOINT=<form recognizer service endpoint>
FORMRECOGNIZER_TEST_API_KEY=<form recognizer API Key>
FORMRECOGNIZER_TRAINING_DATA_CONTAINER_SAS_URL=<SAS url for container with training data>
```

### Setup for perf test runs

```cmd
(env) ~/azure-ai-formrecognizer> pip install -r dev_requirements.txt
(env) ~/azure-ai-formrecognizer> pip install -e .
```

## Test commands

Once `devtools_testutils` is installed, you will have access to the `perfstress` command line tool, which will scan the current module for runable perf tests. Only a specific test can be run at a time (i.e. there is no "run all" feature).

```cmd
(env) ~/azure-ai-formrecognizer> cd tests/perfstress_tests/
(env) ~/azure-ai-formrecognizer/tests/perfstress_tests> perfstress
```
Using the `perfstress` command alone will list the available perf tests found. 

### Common perf command line options
These options are available for all perf tests:
- `--duration=10` Number of seconds to run as many operations (the "run" function) as possible. Default is 10.
- `--iterations=1` Number of test iterations to run. Default is 1.
- `--parallel=1` Number of tests to run in parallel. Default is 1.
- `--warm-up=5` Number of seconds to spend warming up the connection before measuring begins. Default is 5.
- `--sync` Whether to run the tests in sync or async. Default is False (async). This flag must be used for Storage legacy tests, which do not support async.
- `--no-cleanup` Whether to keep newly created resources after test run. Default is False (resources will be deleted).

## Example command
```cmd
(env) ~/azure-ai-formrecognizer/tests/perfstress_tests> perfstress RecognizeCustomForms
```