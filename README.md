# Reproduce the duplicate dependencies issue

## Duplicate Dependencies
This is probably a case that should not occur, but realisticly it can occur. I added this because it is easier to reproduce: Someone installed an incompatible core + vdm.

### Steps to reproduce:
```console
$ npm i @marikaner/test-deps3-core@1.18.0

# time passes... we now need the vdm for some reason
$ npm i @marikaner/test-deps-vdm@^1.19.0
```

### Issue
While we might have decided, that some versions are incompatible due to changes in the generator or similar, an older version of core might still work. Currently it won't work because of duplicate dependencies.

### Solution
Can only be solved by updating the dependencies.

## Duplicate Dependencies 2
Basically the same case as above, but worse, because core + vdm are compatible.

**Steps to reproduce:**
```console
$ npm i @marikaner/test-deps3-core@1.18.0 # or ^1.18.0 some time in the past

# time passes... we now need the vdm for some reason

$ npm i @marikaner/test-deps-vdm@^1.19.0
$ npm update @marikaner/test-deps3-core
```

### Issue
When you delete the node modules or package-lock.json, you are still stuck with this problem.

### Solution
This can be solved by deleting node modules + package-lock.json.

