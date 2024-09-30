# Network Call

## Fetch

1. Get Call

```js
const api_response = await fetch("http://localhost:8000/api/student");
```

2. Post Call

```js
const studentRes = await fetch("http://localhost:8000/api/student", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({ email, fnm, lnm, standard, division }),
});
```

- Use FormData for body

```js
const fd = new FormData();
fd.append("key", value);
// fd.append("file", input.files[0]);
const studentRes = await fetch("http://localhost:8000/api/student", {
  method: "POST",
  headers: {
    // add other headers
  },
  body: fd,
});
```

3. Response

- Some response values

```js
console.log(
  studentRes,
  studentRes.status,
  studentRes.statusText,
  studentRes.headers,
  studentRes.headers.get("Content-Type")
);
```

4. Json Response

```js
const studentResData = await studentRes.json();
```

## Axios Library

1. Installation

```bash
npm install axios
```

2. GET Method Call

- Call

```js
const axiosGetResponse = await axios.get(
  "http://localhost:8000/api/student?page=1&limit=2"
);
```

- Call

```js
const axiosGetResponse = await axios.get("http://localhost:8000/api/student", {
  params: {
    limit: 2,
    page: 1,
  },
});
```

- Response Values

```js
setResponseValues({
  status: axiosGetResponse.status,
  statusText: axiosGetResponse.statusText,
  contentType: axiosGetResponse.headers.get("Content-Type"),
  data: axiosGetResponse.data,
  dataText: JSON.stringify(axiosGetResponse.data),
});
```

3. POST Method Call

- Call

```js
const axiosPostResponse = await axios.post(
  "http://localhost:8000/api/student",
  {
    fnm: "Fred",
    lnm: "Flintstone",
  }
);
```

- call

```js
let data = JSON.stringify({
  fnm: "fnm",
  lnm: "lnm",
});
const axiosPostResponse = await axios.post(
  "http://localhost:8000/api/student",
  data,
  {
    headers: {
      "Content-Type": "application/json",
    },
  }
);
```

- Call

```js
var fd = new FormData();
formData.append("file", imageFile.files[0]);
axios.post("<URL>", formData, {
  headers: {
    "Content-Type": "multipart/form-data",
  },
});
```

- Response Values

```js
setResponseValues({
  status: axiosPostResponse.status,
  statusText: axiosPostResponse.statusText,
  contentType: axiosPostResponse.headers.get("Content-Type"),
  data: axiosPostResponse.data,
  dataText: JSON.stringify(axiosPostResponse.data),
});
```
