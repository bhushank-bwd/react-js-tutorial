# Draggable

## `Drag.jsx`

1. State

```js
const [draggedIconIndex, setDraggedIconIndex] = useState(null);
const [list, setList] = useState([
  { title: "First", index: 1 },
  { title: "Second", index: 2 },
  { title: "Third", index: 3 },
  { title: "Fourth", index: 4 },
  { title: "Fifth", index: 5 },
]);
```

2. Drag Functions

```js
const handleDragStart = (index) => {
  setDraggedIconIndex(index); // set index of selected/dragged element
};
const handleDragOver = (e, index) => {
  e.preventDefault(); // Allow drop by preventing default behavior
};
const handleDrop = (index) => {
  const newIcons = [...list]; // copy/duplicate list
  const [draggedIcon] = newIcons.splice(draggedIconIndex, 1); // remove dragged element
  newIcons.splice(index, 0, draggedIcon); // add dragged element to new index

  // update array by new index
  const updatedArr = newIcons.map((obj, index) => {
    let sequence_no = String(index + 1);
    if (obj.index !== sequence_no) {
      // if index/sequence number is not same then update for current object
      obj.index = sequence_no;
    }
    return obj;
  });
  setList(updatedArr);
};
```

3. JSX

```js
<div className="flex flex-row">
  {list.map((item, index) => {
    return (
      <div
        id={`draggable-div-${index}`}
        draggable
        onDragStart={() => handleDragStart(index)} // Start dragging
        onDragOver={(e) => handleDragOver(e, index)} // Allow drag over this element
        //   onDragLeave={() => handleDragLeave(index)}
        onDrop={() => handleDrop(index)}
        className="w-32 h-32 m-1 bg-gray-400"
        key={item.index}
      >
        {index}-{item.title}
      </div>
    );
  })}
</div>
```
