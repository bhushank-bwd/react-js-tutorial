# Image Crop

## Package

```bash
npm i react-image-crop
```

## Select Image

```jsx
const fileRef = useRef(null);

<button onClick={() => { fileRef.current.click(); }}>Select Profile Picture</button>

<input type="file" className="absolute -z-10" ref={fileRef} accept="image/*" onChange={onSelectFile}/>

const MIN_DIMENSION = 150;
const [imgSrc, setImgSrc] = useState("");


const onSelectFile = (e) => {
    const file = e.target.files?.[0];
    if (!file) return;

    const reader = new FileReader();
    reader.addEventListener("load", () => {
        const imageElement = new Image();
        const imageUrl = reader.result?.toString() || "";
        imageElement.src = imageUrl;

        imageElement.addEventListener("load", (e) => {
        if (error) setError("");
        const { naturalWidth, naturalHeight } = e.currentTarget;
        if (naturalWidth < MIN_DIMENSION || naturalHeight < MIN_DIMENSION) {
            setError("Image must be at least 150 x 150 pixels.");
            return setImgSrc("");
        }
        });
        setImgSrc(imageUrl);
    });
    reader.readAsDataURL(file);
};
```

## Show Cropper Element

```jsx
import ReactCrop, {
  centerCrop,
  convertToPixelCrop,
  makeAspectCrop,
} from "react-image-crop";
const ASPECT_RATIO = 1;
const [crop, setCrop] = useState();
const imgRef = useRef(null);
{
  imgSrc ? (
    <div className="flex flex-col items-center">
      <ReactCrop
        crop={crop}
        onChange={(pixelCrop, percentCrop) => setCrop(percentCrop)}
        circularCrop
        keepSelection
        aspect={ASPECT_RATIO}
        minWidth={MIN_DIMENSION}
      >
        <img
          ref={imgRef}
          src={imgSrc}
          alt="Upload"
          className="w-64 h-88 m-auto"
          onLoad={onImageLoad}
        />
      </ReactCrop>
    </div>
  ) : (
    <>
      <img src="/img/dp.png" className="w-64 h-64 m-auto" />
    </>
  );
}
const onImageLoad = (e) => {
  const { width, height } = e.currentTarget;
  const cropWidthInPercent = (MIN_DIMENSION / width) * 100;

  const crop = makeAspectCrop(
    {
      unit: "%",
      width: cropWidthInPercent,
    },
    ASPECT_RATIO,
    width,
    height
  );
  const centeredCrop = centerCrop(crop, width, height);
  setCrop(centeredCrop);
};
```

## Show Cropped Image

```jsx
const previewCanvasRef = useRef(null);
{
  crop && (
    <div className="w-full text-center">
      <canvas
        ref={previewCanvasRef}
        className="mt-4 m-auto"
        style={{
          border: "1px solid black",
          objectFit: "contain",
          width: 150,
          height: 150,
          display: "none",
        }}
      />
    </div>
  );
}
```

## Perform Crop Action

- Action

```js
setCanvasPreview(
  imgRef.current,
  previewCanvasRef.current,
  convertToPixelCrop(crop, imgRef.current.width, imgRef.current.height)
);
const dataUrl = previewCanvasRef.current.toDataURL("image/png");
setOutputImg(dataUrl);
const tempImg = dataURItoBlob(dataUrl);
```

- setCanvasPreview may be in another file

```js
const setCanvasPreview = (
  image, // HTMLImageElement
  canvas, // HTMLCanvasElement
  crop // PixelCrop
) => {
  const ctx = canvas.getContext("2d");
  if (!ctx) {
    throw new Error("No 2d context");
  }

  // devicePixelRatio slightly increases sharpness on retina devices
  // at the expense of slightly slower render times and needing to
  // size the image back down if you want to download/upload and be
  // true to the images natural size.
  const pixelRatio = window.devicePixelRatio;
  const scaleX = image.naturalWidth / image.width;
  const scaleY = image.naturalHeight / image.height;

  canvas.width = Math.floor(crop.width * scaleX * pixelRatio);
  canvas.height = Math.floor(crop.height * scaleY * pixelRatio);

  ctx.scale(pixelRatio, pixelRatio);
  ctx.imageSmoothingQuality = "high";
  ctx.save();

  const cropX = crop.x * scaleX;
  const cropY = crop.y * scaleY;

  // Move the crop origin to the canvas origin (0,0)
  ctx.translate(-cropX, -cropY);
  ctx.drawImage(
    image,
    0,
    0,
    image.naturalWidth,
    image.naturalHeight,
    0,
    0,
    image.naturalWidth,
    image.naturalHeight
  );

  ctx.restore();
};
export default setCanvasPreview;
```

- Data URI to Blob

```js
const dataURItoBlob = (dataURI) => {
  const byteString = atob(dataURI.split(",")[1]);
  const mimeType = dataURI.split(",")[0].split(":")[1].split(";")[0];
  const arrayBuffer = new ArrayBuffer(byteString.length);
  const intArray = new Uint8Array(arrayBuffer);
  for (let i = 0; i < byteString.length; i++) {
    intArray[i] = byteString.charCodeAt(i);
  }
  const blob = new Blob([arrayBuffer], { type: mimeType });
  return blob;
};
```
