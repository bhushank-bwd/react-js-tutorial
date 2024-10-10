# Form Validation `react-hook-form`

## package

```bash
npm install react-hook-form
```

## Component

1. Import

```js
import { useForm } from "react-hook-form";
```

2. Hook

```js
const {
  register,
  handleSubmit,
  formState: { errors },
} = useForm();
```

```js
const { register, handleSubmit, formState } = useForm();
```

3. Input

```js
<input
  {...register("username", {
    // required: true,
    required: "Please enter username",

    min: 3,
  })}
  className="border border-black p-1 m-1 rounded-md text-black"
  type="text"
></input>;
{
  errors.username?.message && (
    <span className="text-red-600">{errors.username?.message} </span>
  );
}
{
  errors.username?.type == "required" && (
    <span className="text-red-600">Username Required</span>
  );
}
{
  errors.username?.type == "min" && (
    <span className="text-red-600">Username min:3 character required</span>
  );
}
```

4. Custom message

```js
<input
  {...register("username", {
    required: "Please enter username",
    pattern: {
      value: /^[a-zA-Z0-9_]*$/,
      message: "Username should be alphanumeric without special characters",
    },
    minLength: {
      value: 3,
      message: "Username must be at least 3 characters long",
    },
  })}
  className="border border-black p-1 m-1 rounded-md text-black"
  type="text"
></input>;
{
  errors.username?.message && (
    <span className="text-red-600">{errors.username?.message} </span>
  );
}
```

5. List of validation rules supported:

   - required
   - min
   - max
   - minLength
   - maxLength
   - pattern
   - validate

## Schema Validation

1. Install packages

```bash
npm i @hookform/resolvers
npm i yup
```

2. Hook

```js
const schema = yup
  .object({
    username: Yup.string()
      .required("Enter username")
      .min(3, "Min 3 character please")
      .matches(/^[a-zA-Z0-9_]*$/, "Enter valid username"),

    age: Yup.number("valid number")
      .positive("Please Positive Number")
      .integer("valid integer number")
      .required("Mandatory Field"),
    email: Yup.string().email("Please valid mail"),
    skills: Yup.string().required("Select Skills"),
  })
  .required();

const {
  register,
  handleSubmit,
  formState: { errors },
} = useForm({ resolver: yupResolver(schema) });
```

3. Input (Same for select)

```js
<input
  {...register("age")}
  className="border border-black p-1 m-1 rounded-md text-black"
  type="text"
></input>;
{
  errors.age?.message && (
    <span className="text-red-600">{errors.age?.message}</span>
  );
}
```

4. on submit

```js
<form onSubmit={handleSubmit(formSubmit)}></form>
```

```js
const formSubmit = (data) => console.log(data);
```
