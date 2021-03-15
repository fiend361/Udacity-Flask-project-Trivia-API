# Full Stack Trivia API Backend

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py.

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server.

## Database Setup

With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:

```bash
psql trivia < trivia.psql
```

## Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application.

## Tasks

One note before you delve into your tasks: for each endpoint you are expected to define the endpoint and response data. The frontend will be a plentiful resource because it is set up to expect certain endpoints and response data formats already. You should feel free to specify endpoints in your own way; if you do so, make sure to update the frontend or you will get some unexpected behavior.

1. Use Flask-CORS to enable cross-domain requests and set response headers.
2. Create an endpoint to handle GET requests for questions, including pagination (every 10 questions). This endpoint should return a list of questions, number of total questions, current category, categories.
3. Create an endpoint to handle GET requests for all available categories.
4. Create an endpoint to DELETE question using a question ID.
5. Create an endpoint to POST a new question, which will require the question and answer text, category, and difficulty score.
6. Create a POST endpoint to get questions based on category.
7. Create a POST endpoint to get questions based on a search term. It should return any questions for whom the search term is a substring of the question.
8. Create a POST endpoint to get questions to play the quiz. This endpoint should take category and previous question parameters and return a random questions within the given category, if provided, and that is not one of the previous questions.
9. Create error handlers for all expected errors including 400, 404, 422 and 500.

## API Endpoints Documentation

### Endpoints

```GET '/categories'
GET '/categories/<certain_category_id>/questions'
GET '/questions'
POST '/questions'
DELETE '/questions/<certain_question_id>'
POST '/questions/search'
POST 'quizzes'
```

### GET '/categories'

- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request Arguments: None
- Returns: An object with a single key, categories, that contains a object of id: category_string key:value pairs.

```{
    '1' : "Science",
    '2' : "Art",
    '3' : "Geography",
    '4' : "History",
    '5' : "Entertainment",
    '6' : "Sports"
}
```

### GET '/categories/<certain_category_id>/questions'

- Fetches all the questions that have the category id certain_category_id
- Request Arguments: None
- Returns: A list of objects each resembling a question. Response has the following format:

```{
    'success': True,
    'questions': [{
            'id': 1,
            'question': 'question1',
            'answer': 'answer to question1',
            'category': 6,
            'difficulty': 4
        },
        {
            'id': 12,
            'question': 'question12',
            'answer': 'answer to question12',
            'category': 6,
            'difficulty': 1
    }],
    'total_questions': 2,
    'current_category': 6
}
```

### GET '/questions'

- Fetches all the questions
- Request Arguments: None
- Returns: A list of all questions and the category object. Response has the following format:

```{
    'success': True,
    'questions': [{
            'id': 1,
            'question': 'question1',
            'answer': 'answer to question1',
            'category': 6,
            'difficulty': 4
        },
        {
            'id': 2,
            'question': 'question2',
            'answer': 'answer to question2',
            'category': 3,
            'difficulty': 1
    }],
    'total_questions': 2,
    'categories': {
        '1' : "Science",
        '2' : "Art",
        '3' : "Geography",
        '4' : "History",
        '5' : "Entertainment",
        '6' : "Sports"
    }
}
```

### POST '/questions'

- Creates a new question.
- Request arqument: the question object with the following format:

```{
  'question': 'the question',
  'answer': 'the answer',
  'category': 3,
  'difficulty': 1
  }
```

- Returns: the id of the created question and the new questions. Response has the following format:

```{
  'success': True,
  'created': 22,
  'questions': [{}, {}, ],
  'total_questions': 5
  }
```

### DELETE '/questions/<certain_question_id>'

- Deletes the question with the id certain_question_id
- Request arqument: None.
- Returns: the id of the deleted question and the new questions. Response has the following format:

```{
  'success': True,
  'deleted': 22,
  'questions': [{}, {}, ],
  'total_questions': 4
  }
```

### POST '/questions/search'

- Searches for questions contain a search term.
- Request arqument: the search term with the format:

```{
  'searchTerm': 'your search term'
  }
```

- Returns: the questions that contain the search term. Response has the following format:

```{
  'success': True,
  'questions': [{}, {}, ],
  'total_questions': 4
  }
```

### POST 'quizzes'

- Fetches a new random question with a given category that is not in a list of previous questions.
- Request arqument: a list of the ids of the previous questions and a given category. Format:

```{
  'previous_questions': [1, 5, 6, 8],
  'quiz_category': 6
  }
```

- Returns: a single random question with the given category and that is not in the list of previous questions. Response has the following format:

```{
  'success': True,
  'question': {}
  }
```

## Testing

To run the tests, run

```dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```
