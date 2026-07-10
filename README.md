# GitHub Actions

## ruby-ci

The ruby-ci action is used for running RSpec tests on Ruby projects using a matrix strategy.

Each run in the matrix can specify a ruby version to use and optional Appraisal Gemfile to use.

You can also run the the standardrb and YARD tasks to verify code and documentation standards are met.

You can also specify a version of bundler to use if the project requires a specific version with the `bundler` value.

```yaml
jobs:
  specs:
    name: Run specs
    runs-on: ubuntu-latest
    strategy:
      fail-fast: false
      matrix:
        include:
          - ruby: "ruby"
            standardrb: true
            yard: true
          - ruby: "3.4"
            appraisal: "activerecord_8"
          - ruby: "3.3"
            appraisal: "activerecord_8.0"
          - ruby: "3.2"
            appraisal: "activerecord_7"
          - ruby: "3.1"
            appraisal: "activerecord_7.0"
    steps:
      - name: Checkout
        uses: actions/checkout@v6
      - name: Ruby CI
        uses: bdurand/github-actions/ruby-ci@main
        with:
          ruby: ${{ matrix.ruby }}
          appraisal: ${{ matrix.appraisal }}
          bundler: ${{ matrix.bundler }}
          standardrb: ${{ matrix.standardrb }}
          yard: ${{ matrix.yard }}
```
