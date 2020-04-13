# TEST

## Test Pyramid

![Test Pyramid](https://res.cloudinary.com/practicaldev/image/fetch/s--tjTcgZaD--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://alysivji.github.io/images/30-39/test_pyramid.png)

## Tools

- http://appium.io/
- http://selendroid.io/
- https://calaba.sh/

## Unit Test

[Link to the Note](./unit-test.md)

## Integration Test

Every complex application has internal and external components working together to do something interesting. In contrast to units tests which focus on individual components, integration tests combine various parts of the system and test them together as a group. Integration testing can also refer to testing at service boundaries of our application, i.e. when it goes out to **the database, file system, or external API.**

### Integration Test Example

Our func gets data and save it in db. Our test, runs the func and check it with db after that to see if our func worked properly or not.

```py
def save_to_db(url, top_word):
    record = TopWord()
    record.url = url
    record.word = top_word[0]
    record.num_occurrences = top_word[1]

    db.session.add(record)
    db.session.commit()

    return record

def test_save_to_db():
    url = "http://test_url.com"
    most_common_word_details = ("Python", 42)

    word = save_to_db(url, most_common_word_details)

    inserted_record = TopWord.query.get(word.id)
    assert inserted_record.url == "http://test_url.com"
    assert inserted_record.word == "Python"
    assert inserted_record.num_occurrences == 42
```

## EndToEnd Test

End-to-end tests check to see if the system meets our defined business requirements. A common test is to trace a path through the system in the same manner a user would experience. For example, we can test a new user workflow: simulate creating an account, "clicking" the link in the activate email, logging-in for the first time, and interacting with our web application's tutorial modal pop-up.

We can conduct end-to-end tests through our user interface (UI) by leveraging a browser automation tool like Selenium. This creates a dependency between our UI and our tests, which makes our tests brittle: a change to the front-end requires us to change tests. This is not sustainable as either our front-end will become static or our tests will not be run.

A better solution is to test the subcutaneous layer, i.e. the layer just below our user interface. For a web application, this would be testing the REST API, both sending in JSON and getting JSON out.

End-to-end tests are considered black box as we do not need to know anything about the implementation in order to conduct testing. This also means that test failures provide no indication of what went wrong; we would need to use logs to help us trace the error and diagnose system failure.

### End-to-End Test Example

Here we are using the Flask Test client to run subcutaneous testing on our REST API. There are a lot of things happening behind the scene and the result we get back (HTTP status code) lets us know that the test either passed or failed.

```py
def test_end_to_end():
    client = app.test_client()

    body = {"url": "https://www.python.org"}
    response = client.post("/top-word", json=body)

    assert response.status_code == HTTPStatus.OK
```

## Load Test

## Lab Test

## Memory leaking Test

## Stress Test

## Interruption Test

## functional Testing

```

```
