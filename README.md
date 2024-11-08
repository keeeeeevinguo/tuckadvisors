# GPT Analysis API

This API allows users to access and update an analysis of synergies between two companies generated by the Tuck Advisors custom GPT. It provides endpoints to retrieve the current analysis content and add additional information to it.

## Getting Started

### Dependencies
* **Python 3**
* **Flask** 
* **SQLite**
* **JSON** \
\
**Note**: SQLite and Json come installed as part of the Python standard library. If necessary, install Flask by running:

```bash
  pip install flask
  ```

### Installing
1. Clone this project or download the `TuckApi.py` file to your local machine.
2. The database will be automatically initialized with the initial JSON content the first time the program is run.

### Executing Program
To run the API server:

1. Open a terminal.
2. Navigate to the project directory.
3. Run the following command to start the Flask server:
   ```bash
   python TuckApi.py
   ```
4. Once started, the server will run at `http://127.0.0.1:5000`.

### API Endpoints

#### GET `/api/tuckapi`

* Retrieves the current gptOutput.
* **URL**: `http://127.0.0.1:5000/api/tuckapi`
* **Method**: `GET`
* **Response**: JSON object containing the current gptOutput.

Example response:
```json
{
  "gptOutput": "Initial analysis content generated between ABC LLC and Preppy LLC..."
}
```

#### POST `/api/tuckapi`

* Adds a new sentence to the existing gptOutput.
* **URL**: `http://127.0.0.1:5000/api/tuckapi`
* **Method**: `POST`
* **Body**: JSON object containing the text to add.
  ```json
  {
    "text": "This is an additional sentence."
  }
  ```
* **Response**: JSON object with a confirmation message and updated gptOutput.

Example response:
```json
{
  "message": "gptOutput updated successfully with new text: This is an additional sentence."
}
```

## Testing the API

### 1. Test `GET` Request

Open `http://127.0.0.1:5000/api/tuckapi` in your browser to see the current gptOutput.

### 2. Test `POST` Request

To add new text to the gptOutput, use the following command:

```bash
curl -X POST -H "Content-Type: application/json" -d '{"text": "This is an additional sentence added for testing."}' http://127.0.0.1:5000/api/tuckapi
```

**Expected Output**:
The response should confirm that the gptOutput was updated.

```json
{
  "message": "gptOutput updated successfully with new text: This is an additional sentence added for testing."
}
```

#### Confirm the Update with Another `GET` Request

To verify that the gptOutput includes the newly added sentence, run the `GET` request again:

```bash
curl -X GET http://127.0.0.1:5000/api/tuckapi
```

**Expected Output**:
The response should include the initial gptOutput along with the added sentence.

```json
{
  "gptOutput": "Initial analysis content generated between ABC LLC and Preppy LLC... This is an additional sentence added for testing."
}
```

#### Test `POST` Request with Empty Text (Error Case)

To test the error handling, try sending a `POST` request with an empty `text` field:

```bash
curl -X POST -H "Content-Type: application/json" -d '{"text": ""}' http://127.0.0.1:5000/api/tuckapi
```

**Expected Output**:
You should see an error message since the `text` field is empty.

```json
{
  "error": "No text provided"
}
```

## Authors

Kevin Guo
