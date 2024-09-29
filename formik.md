# Fromik Validation

## Package installation

```bash
npm install formik --save
npm install yup
npm i react-select
```

## Package import

```js
import { Field, Form, Formik } from "formik";
import ReactSelect from "react-select";
import * as Yup from "yup";
```

## Formik Component

```js
<Formik
  initialValues={initialValues}
  validationSchema={signUpValidation}
  onSubmit={(values, { resetForm }) => formSubmitFunction(values, resetForm)}
>
  {({ errors }) => <Form></Form>}
</Formik>
```

- initialValues = object initial like {name:'John',email:'john@mail.com'}

## Formik Field

1. Text

```js
<Field
  name="fnm"
  className="border border-black outline-1"
  id="fnm"
  type="text"
/>
```

2. React Select

```js
<Field name="standard" id="standard">
  {({ field, form }) => (
    <ReactSelect
      {...field}
      options={standardOptions}
      placeholder="Select an Standard"
      onChange={(selectedOption) =>
        form.setFieldValue("standard", selectedOption)
      }
    />
  )}
</Field>
```

3. Error

```js
{
  errors.fnm && <small className="text-sm text-red-500">{errors.fnm}</small>;
}
```

## Form Submit function

```js
const formSubmitFunction = (values, resetForm) => {
  console.log("values received", values);
  // form submit operations
  resetForm();
};
```

## Validation using yup

```js
const signUpValidation = Yup.object({
  fnm: Yup.string().min(3).required("Enter first name").max(255),
  email: Yup.string().email("Enter valid email").required("enter email"),
  lnm: Yup.string().min(3).required("Enter Last name").max(255),
  standard: Yup.object().required("Select standard"),
  division: Yup.object().required("Select division"),
});
```
