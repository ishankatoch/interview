> What are fixtures in pytes?

The @pytest.fixture decorator provides an easy yet powerful way to setup and teardown resources for your tests:

```python
class Car:
    def __init__(self, model, year):
        self.model = model
        self.year = year

    def __str__(self):
        return f"Car: {self.model} ({self.year})"


import pytest


@pytest.fixture
def car():
    return Car("Sierra", 2020)


def test_str(car):  # fixtures are passed in as test function arguments assert str(car) == 'Car: Sierra (2020)'
    assert str(car) == 'Car: Sierra (2020)'

```

> How to skip tests based on condition

> Create a temporary directory?

> Use selenium for integration testing?

> parameterized tests in pytest?

> How do you generate code coverage and reporting?
