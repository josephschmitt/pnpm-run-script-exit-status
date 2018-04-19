# PNPM Exit Status Bug

This repo demonstrates a bug with pnpm run-script whereby the exit status is always 0. The
package.json to reproduce this bug is set up with the following scripts:

- `test:exit`: An npm script that just always exits 1
- `test:pnpm`: A `package.json` script that runs the exit script using pnpm
- `test:npm`: A `package.json` script that runs the exit script using npm

## Expected result

Running `test:pnpm` and `test:npm` will both output `STATUS: 1`

## Actual result

Running `test:pnpm` outputs `STATUS: 0` while `test:npm` correctly outputs `STATUS: 1`.

## Impact

This is especially a problem if you break up your testing scripts and run them from test, since it
means unit tests will always pass even if there's an error.
