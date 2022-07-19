# [Support for NPM Workspaces #67](https://github.com/iambumblehead/esmock/issues/67)

This is a bit of a weird one. I've noticed that there are certain scenarios where `esmock` fails with NPM's Workspaces.

I'm not entirely sure where to start with this particular issue, though. But I went ahead and [created an example repo](https://github.com/Swivelgames/esmock-issue-67) that reproduces the issue.

If you clone the repo, you can reproduce the issue by running the following:
```
npm run setup
npm run test
```

If you're not on a UNIX-based system, you can run the commands manually:
```
git submodule init
git submodule update
cd esmock
git apply ../add-tests.patch
cd ..
npm install
npm run --workspace=esmock test
```

Notice the following failure:

```diff
    # Subtest: should mock a node_module
    not ok 17 - should mock a node_module
      ---
      duration_ms: 0.028361695
      failureType: 'testCodeFailure'
      error: |-
        Expected values to be strictly equal:
        + actual - expected

        + 'not_mocked'
        - 'foobar'
      code: 'ERR_ASSERTION'
      stack: |-
        TestContext.<anonymous> (file:///home/jdalrymple/src/by-project/esmock-ws/esmock/spec/node/esmock.node.test.js:226:10)
        async Test.run (node:internal/test_runner/test:338:9)
        async Test.processPendingSubtests (node:internal/test_runner/test:158:7)
      ...
```
