## bbb-ci-test-resources

Repository for puppeteer media browser files and visual regressions tests.

## Why this repository ?

This repository contains files with big sizes (images, video, audio and pdf). These files will be called in the execution of the tests with our without Visual Regressions.

This repository link is included in [import-tests-ci-resources.sh#L6](https://github.com/bigbluebutton/bigbluebutton/blob/develop/bigbluebutton-html5/tests/puppeteer/import-tests-ci-resources.sh#L6).

Test files are located cordinately with what version they will be used for; For 2.3 testing: it's files are located in `2.3` folder. And future BBB versions with different layouts will have different folders.

## How to use ?

In Audio, Webcam, Presentation File Upload and Visual Regressions tests. Our tests scripts require ready to use files, to guarantee the expected results.

For example: [page.js#L198-L208](https://github.com/bigbluebutton/bigbluebutton/blob/develop/bigbluebutton-html5/tests/puppeteer/core/page.js#L198-L208)

```
const args = [
    '--no-sandbox',
    '--use-fake-ui-for-media-stream',
    '--use-fake-device-for-media-stream',
    '--window-size=1280,720',
    `--use-file-for-fake-audio-capture=${path.join(__dirname, '../media/audio.wav')}`,
    '--allow-file-access',
    '--lang=en-US',
];
```

In the code block above, `--use-file-for-fake-audio-capture=${path.join(__dirname, '../media/audio.wav')}` is importing `audio.wav` to use it as audio capture source to test audio in a BBB session.

## How this is going to be used in CI ?

Running automated tests with CI will require to have the testing resources files ready to use, and for this reason this repository was created.

For example: In Visual Regressions, CI will need to compare visual differences between ready to use screenshots and the new taken ones in test execution. Why? because CI takes a long time to execute tests, and even longer if we are going to let it collect the screenshot it will need in a test by itself and rerun same test again to compare between screenshot collected and screenshot taken in the reexecution.

