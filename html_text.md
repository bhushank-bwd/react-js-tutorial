# Rendering HTML Text

## In component add following array

```js
const list = [
    "Hello I'm Bhushan<br/><p>I'm Working as Software Developer</p>",
    "<b>Education</b>: BECSE",
    "Current Company: <em>TCS</em>",
];
```

## Map or use above list in following way

- Use prop `dangerouslySetInnerHTML` for html element li

```js
{list.map((item, index) => (
    <li dangerouslySetInnerHTML={{ __html: item }} key= {index} />
))}
```
