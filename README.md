# Image Editor 
An image editor created using HTML, CSS, and JavaScript allows users to make changes to their images. This editor includes buttons for brightness, saturation, inversion, and grayscale filtering, as well as the ability to flip an image in different directions.

# HTML 

```
<body>
	<div class="container disable">
        <h2>Easy Image Editor</h2>
        <div class="wrapper">
            <div class="editor-panel">
                <div class="filter">
                    <label class="title">Filters</label>
                    <div class = "options"> //button options for filter
                        <button id="brightness" class ="active">Brightness</button>
                        <button id="saturation">Saturation</button>
                        <button id="inversion">Inversion</button>
                        <button id="grayscale">Grayscale</button>
                    </div>
                    <div class ="slider">
                        <div class="filter-info">
                            <p class = "name">Brightness</p>
                            <p class = "value">100%</p>
                        </div>
                        <input type="range" value="100" min="0" max="200">
                    </div>
                </div>
                <div class="rotate">
                    <label class="title">Rotate & Flip</label>
                    <div class = "options">
                        <button id="left"><i class = "fa-solid fa-rotate-left"></i></button>
                        <button id="right"><i class = "fa-solid fa-rotate-right"></i></button>
                        <button id="horizontal"><i class = "bx bx-reflect-vertical"></i></button>
                        <button id="vertical"><i class = "bx bx-reflect-horizontal"></i></button>
                    </div>
                </div>
            </div>
            <div class ="preview-img">
                <img src="image-placeholder.svg" alt="preview-img">
            </div>
        </div>
        <div class = "controls">
            <button class = "reset-filter">Reset Filters</button>
            <div class="row">
                <input type="file" class="file-input" accept="image/*" hidden>
                <button class="choose-img">Choose Image</button>
                <button class="save-img">Save Image</button>
            </div>
        </div>
    </div>

    <script src="script.js"></script>

    </body>

```

As shown above is our HTML file where we write the body of our code. The website's contents will be contained within the HTML: buttons for rotation and filter options, as well as a slider for changing the value of the selected filter

Next, lets move onto the CSS file.

# CSS
```
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: sans-serif;
}
body{
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    background: #E3F2FD;
}
.container{
    width: 850px;
    background: #fff;
    border-radius: 10px;
    padding: 30px 35px 35px;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
}
.container.disable :where(.editor-panel, .reset-filter, .save-img){
    opacity: 0.6;
    pointer-events: none;
}
.container h2{
    font-size: 22px;
    font-weight: 500;
}
.container .wrapper{
    display: flex;
    margin: 20px 0;
    min-height: 335px;
}
.wrapper .editor-panel{
    width: 280px;
    padding: 15px 20px;
    border-radius: 5px;
    border: 1px solid #ccc;
}
.editor-panel .title{
    display: block;
    font-size: 16px;
    margin-bottom: 12px;
}
.editor-panel .options, .controls{
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}
.editor-panel button{
    height: 40px;
    font-size: 14px;
    color: #6C757D;
    margin-bottom: 8px;
    border-radius: 3px;
    background: #fff;
    border: 1px solid #aaa;
}
.editor-panel .filter-button{
    width: calc(100% / 2 - 4px);
}
.editor-panel button:hover{
    background: #f5f5f5;
}
.filter button.active{
    color: #fff;
    background: #5372F0;
    border-color: #5372F0;
}
.filter .slider{
    margin-top: 12px;

}
.filter .slider .filter-info{
    display: flex;
    color: #464646;
    font-size: 14px;
    justify-content: space-between;
}
.filter .slider input{
    width: 100%;
    height: 5px;
    accent-color: #5372f0;
}
.editor-panel .rotate{
    margin-top: 17px;
}
.editor-panel .rotate button{
    width: calc(100%/4-3px);
}
.rotate button:nth-child(3)
.rotate button:nth-child(4){
    font-size: 18px;
}
.wrapper .preview-img{
    flex-grow: 1;
    display: flex;
    overflow: hidden;
    align-items: center;
    justify-content: center;
    margin-left: 20px;
}
.preview-img img{
    max-width: 490px;
    max-height: 335px;
    width: 100%;
    height: 100%;
    object-fit: contain;

}
.controls button{
    font-size: 14px;
    cursor: pointer;
    color: #fff;
    background: #fff;
    padding: 11px 20px;
    border-radius: 3px;
    text-transform: uppercase;
}
.controls .reset-filter{
    color: #6C757D;
    border: 1px solid #6C757D;

}
.controls .choose-img{
    background: #6C757D;
    border: 1px solid #6C757D;
}
.controls .save-img{
    background: #5372F0;
    border: 1px solid #5372F0;
    margin-left: 5px;
}


/*for small devices*/
@media screen and (max-width: 760px){
    .container{
        padding: 25px;
    }

    .container .wrapper{
        flex-wrap: wrap-reverse;
    }

    .wrapper .editor-panel{
        width: 100%;
    }
    .wrapper .preview-img{
        width: 100%;
        margin: 0 0 15px;
    }  
}
@media screen and (max-width: 500px) {
    .controls button{
        width: 100%;
        margin-bottom: 10px;
    }
    .controls .row{
        width: 100%;
    }
    .controls .row .save-img{
        margin-left: 0px;
    }  
}



```

The code written in CSS is how the web page will be designed and displayed to users. CSS is used to specify the styles of the web pages, including the design, layout, and variations in display for various devices and screen sizes. 
 

# JS
The essential elements of the website, such as the filter functionality, are contained in this JavaScript file.
```
const fileInput = document.querySelector(".file-input"),
filterOptions = document.querySelectorAll(".filter button"),
filterName = document.querySelector(".filter-info .name"),
filterValue = document.querySelector(".filter-info .value"),
filterSlider = document.querySelector(".slider input"),
rotateOptions = document.querySelectorAll(".rotate button"),
previewImg = document.querySelector(".preview-img img"),
resetFilterBtn = document.querySelector(".reset-filter"),
chooseImgBtn = document.querySelector(".choose-img"),
saveImgBtn = document.querySelector(".save-img");
```

Next is to declare the image constant filter:

```
let brightness = 100, saturation = 100, inversion = 0, grayscale = 0;
let rotate = 0, flipHorizontal= 1, flipVertical = 1;
```

This function is to to display the selected image in the preview image section. The buttons in the website will be able to use after the user has chosen an image to edit.

```
const loadImage = () => {
    let file = fileInput.files[0]; //get user selected file
    if (!file) return; //if user didn't select file
    previewImg.src = URL.createObjectURL(file); //passing file url as preview img 
    previewImg.addEventListener("load", () => {
        resetFilterBtn.click(); //when select new img, it will reset all of the filters
        document.querySelector(".container").classList.remove("disable");
    });
}
```

We will need a function to highlight a specific button we clicked, lets say "brightness", hence the use of **active**. Apart of that, with the fuction **innerText** the filter name will be changed according to the button clicked as well as the filter slider value. 
```
filterOptions.forEach(option => {
    option.addEventListener("click",()=>{
        document.querySelector(".filter .active").classList.remove("active");
        option.classList.add("active")
        filterName.innerText = option.innerText;
        //add max num for each filter option
        if(option.id === "brightness"){
            filterSlider.max = "200";
            filterSlider.value = brightness;
            filterValue.innerText = `${brightness}%`;
        }else if(option.id === "saturation"){
            filterSlider.max = "200";
            filterSlider.value = saturation;
            filterValue.innerText = `${saturation}%`;
        }else if(option.id === "inversion"){
            filterSlider.max = "100";
            filterSlider.value = inversion;
            filterValue.innerText = `${inversion}%`;
        }else {
            filterSlider.max = "100";
            filterSlider.value = grayscale;
            filterValue.innerText = `${grayscale}%`;
        }
```

After we have set the filter value, we will need to update the image accordingly: 
```
const updateFilter = () => {
    filterValue.innerText= `${filterSlider.value}%`;
    const selectedFilter = document.querySelector(".filter .active"); //getting selected filter btn

    if(selectedFilter.id === "brightness"){
        brightness = filterSlider.value;
    } else if(selectedFilter.id === "saturation"){
        saturation = filterSlider.value;
    }

    else if (selectedFilter.id ==="inversion"){
        inversion = filterSlider.value;
    }

    else{
        grayscale = filterSlider.value;
    }
    applyFilters();
```

Image will be altered using `tranform` for rotation of image and `filter` for visual changes. 

```
const applyFilters = () => {
    previewImg.style.transform = `rotate(${rotate}deg) scale(${flipHorizontal} , ${flipVertical}`;
    previewImg.style.filter= `brightness(${brightness}%) saturate(${saturation}%) invert(${inversion}%) grayscale(${grayscale}%)`;
}
```

**Function to Rotate Picture**

```
    rotateOptions.forEach(option => {
    option.addEventListener("click",()=>{
        if (option.id === "left"){
            rotate -= 90; //decrement left rotate value by -90; img turn left
        }
        else if (option.id === "right"){
            rotate += 90; //increment right rotate value by -90; img turn right
        }
        else if (option.id === "horizontal"){
            //if flipHorizontal value is 1, set the value to -1 else set 1
            flipHorizontal = flipHorizontal === 1 ? -1 : 1; 
            
        }

        else {
            //if flipVertical value is 1, set the value to -1 else set 1
            flipVertical = flipVertical === 1 ? -1 : 1; 
            
        }
        applyFilters();
```

**Reset all variable value to its default value.**
```
const resetFilter = () => {
brightness = 100; saturation = 100; inversion = 0; grayscale = 0;
rotate = 0; flipHorizontal= 1; flipVertical = 1;
filterOptions[0].click(); //clicking brightness btn, so brightness selected bt default
applyFilters();
}
```

Our last step is to add a function that will enable us to save our edited image. Here we shall use `canvas` to download our image. 

```
const saveImage = () => {
    const canvas = document.createElement("canvas"); //creating canvas element
    const ctx = canvas.getContext("2d"); //canvas.getContext return a drawing context on the canvas
    canvas.width = previewImg.naturalWidth; //set canvas width to actual img width
    canvas.height = previewImg.naturalHeight; //set canvas height to actual img height

    //apply selected filter in img to canvas
    ctx.filter = `brightness(${brightness}%) saturate(${saturation}%) invert(${inversion}%) grayscale(${grayscale}%)`;
    ctx.translate(canvas.width / 2, canvas.height / 2); //translating canvas from center
    if (rotate !==0){ //if rotate value isn't 0, rotate the canvas
        ctx.rotate(rotate*Math.PI/180);

    }


    ctx.scale(flipHorizontal, flipVertical); //flip canvas, horizontal/vertical
    ctx.drawImage(previewImg, -canvas.width / 2, -canvas.height / 2, canvas.width, canvas.height);
   
    const link = document.createElement("a"); //creating <a> element
    link.download = "image.jpg"; //passing <a> tag download value to "image.jpg"
    link.href = canvas.toDataURL(); //passing <a> tag href value to canvas data url
    link.click(); //clicking <a> tag so the image download
}
```

Before that, let's not forgot to insert `addEventListener()` method to our code so it will function properly. This method is added to call functions when a specific button is click such as the **Save Image** button. 

```
fileInput.addEventListener("change",loadImage);
filterSlider.addEventListener("input", updateFilter);
resetFilterBtn.addEventListener("click", resetFilter);
saveImgBtn.addEventListener("click", saveImage);
chooseImgBtn.addEventListener("click",() => fileInput.click());
```

Now we are done with our website!


