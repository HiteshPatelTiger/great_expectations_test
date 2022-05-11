---
title: Code style guide
---

:::info Note
This style guide will be enforced for all incoming PRs. However, certain legacy areas within the repo do not yet fully adhere to the style guide. We welcome PRs to bring these areas up to code.
:::

### Code

* **Methods are almost always named using snake_case.**

* **Methods that behave as operators (e.g. comparison or equality) are named using camelCase.** These methods are rare and should be changed with great caution. Please reach out to us if you see the need for a change of this kind.

* **Experimental methods should log an experimental warning when called:** “Warning: some_method is experimental. Methods, APIs, and core behavior may change in the future.”

* **Experimental classes should log an experimental warning when initialized:** “Warning: great_expectations.some_module.SomeClass is experimental. Methods, APIs, and core behavior may change in the future.”

* **Docstrings are highly recommended.** We use the Sphinx’s [Napoleon extension](http://www.sphinx-doc.org/en/master/ext/napoleon.html) to build documentation from Google-style docstrings.

### Linting

Our CI system will check using `black`, `isort`, `flake8` and `pyupgrade`. 

Linting with `isort` MUST occur from a virtual environment that has all required packages installed, and pre-commit uses the virtual environment from which it was installed, whether or not that environment is active when making the commit. 

This means you must ensure you have activated a virtual environment that has all development requirements installed **before running `pre-commit install`**.

```console
pre-commit uninstall
# ACTIVATE ENV, e.g.: conda activate pre_commit_env OR source pre_commit_env/bin/activate
pip install -r requirements-dev.txt
pre-commit install --install-hooks
```

If you have already committed files but are seeing errors during the continuous integration tests, you can run tests manually:

```console
black <PATH/TO/YOUR/CHANGES>
isort <PATH/TO/YOUR/CHANGES> --check-only --skip docs
flake8 <PATH/TO/YOUR/CHANGES>
pyupgrade <PATH/TO/YOUR/CHANGES> --py3-plus
```

### Expectations

* **Use unambiguous Expectation names**, even if they’re a bit longer, e.g. `expect_columns_to_match_ordered_list` instead of `expect_columns_to_be`.

* **Avoid abbreviations**, e.g. `column_index` instead of `column_idx`.

* **Expectation names should be prefixed to reflect their base classes:**

| Base class                   |  prefix                         |
|------------------------------|---------------------------------|
| `Expectation`                |  `expect_...`                   | 
| `TableExpectation`           |  `expect_table_...`             | 
| `ColumnMapExpectation`       |  `expect_column_values_...`     | 
| `ColumnAggregateExpectation` |  `expect_column_...`            | 
| `ColumnPairMapExpectation`   |  `expect_column_pair_values...` | 
| `MultiColumnMapExpectation`  |  `expect_multicolumn_values...` | 

