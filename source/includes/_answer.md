# Answer

## Submit an answer

> Your request:

```javascript
const {
  surveyExecutionId,
  userGuid,
  flyerCode
} = getSurveyExecutionDetails();

const response = await axios.post(`/answer/${flyerCode}`, {
  text: "This is my answer",
  survey_execution_id: surveyExecutionId,
  user_guid: userGuid,
  question_id: 2
});
```

> The above request returns JSON structured like this:

```json
 {
  "id": 19,
  "question_id": 2,
  "survey_execution_id": 7,
  "question_answer_id": null,
  "created_at": "2021-10-22T12:36:20.721Z",
  "updated_at": "2021-10-22T12:36:20.722Z",
  "text": "This is my answer"
}
```

Call this endpoint for every question in a survey execution. You need to pass in the survey_execution_id and user_guid
that was given to you on requesting the questions initially. Bear in mind if there is already an answer saved for a
question within the same survey execution, this will be overwritten as the main answer (any unique previous answers are stored).

### HTTP Request

`GET /answer/:flyerCode`

### Query Body

Prop | Required | Type | Description
--------- | -------- | ---- | ---------
text | false | string | Text value of the answer - this is used unless the question is multiple choice
question_answer_id | false | number | Multiple choice answer id
survey_execution_id | true | number | id given upon requesting survey questions
user_guid | true | string | guid given up requesting survey questions (this should be persisted on device permanently)
question_id | true | number | id of the question that the answer refers to
