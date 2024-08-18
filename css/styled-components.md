# Styled Components

## Installation

- Run Command

```bash
npm i styled-components
```

## Component `src\Button.jsx`

```js
import { styled } from "styled-components";
const Button = ({ label = "Button Text" }) => {
  const Btn = styled.button`
    background-color: ${({ btnType }) =>
      btnType == "success" ? "green" : "red"};
    color: #fff;
    margin: 5px;
    border: 1px solid transparent;
    padding: 7px;
    border-radius: 6px;

    &:hover {
      background-color: #fff;
      color: ${({ btnType }) => (btnType == "success" ? "green" : "red")};
      border: 1px solid ${({ btnType }) =>
          btnType == "success" ? "green" : "red"};
    }
    & span {
      text-decoration: line-through;
    }
  `;
  return (
    <Btn btnType="success">
      {label} <span>This is nested style in styled component</span>{" "}
    </Btn>
  );
};
export default Button;
```

## Advantages

1. Quick and Easy Load
2. Scoped

## Disadvantage

1. No clean separation of css and jsx
2. Small wrapper components
