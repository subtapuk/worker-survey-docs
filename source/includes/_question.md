
# Question

## Request Questions

> Your request:

```javascript
const flyerCode = getFlyerCode();
const userId = getUserId();
const response = await axios.get(`/question/${flyerCode}?user_id=${userId}`);
```

> The above request returns JSON structured like this:

```json
{
  "survey_execution_id": 24,
  "user_id": "yourUserId",
  "questions": [
    {
      "id": 2,
      "text": "What's your favourite color?",
      "created_at": "2019-03-03 12:10:230",
      "prompts": "Think about what makes you happy, what makes you sad",
      "placeholder": "Choose your color here",
      "question_type": {
        "name": "select",
        "id": 1
      },
      "question_answers": [
        {
          "id": 1,
          "question_id": 2,
          "text": "red"
        },
        {
          "id": 2,
          "question_id": 2,
          "text": "blue"
        }
      ]
    }
  ]
}
```

This endpoint should be called on opening of the survey to begin a survey execution. Make sure to save survey_execution_id
in session storage to capture all answers within a single session - user_id is intended to be persisted between survey
executions, i.e. in local storage.

Some notes on the returned questions:

- prompts and placeholder are both optional values
- question_answers refers to available answers when a survey question has limited answers (e.g a multi-select question)

### HTTP Request

`GET /question/:flyerCode`

### Query Parameters

Parameter | Required | Description
--------- | -------- | ------- 
user_id | false | user_id saved in localstorage from previous form executions - if not passed in a new user will be created



