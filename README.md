# Image Editor 
A photo editor made with HTML, CSS, and JavaScript. User can apply filters to their images, such as grayscale, inversion, saturation, and brightness adjustments as well as flip or rotate the images and save their edited versions in their laptop.

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

As shown above is our HTML file where we write the body of our code. In here are the buttons needed in the Image Editor webpage. A slider is also added for us to increase or decrease the amount of the filter button we selected.

Next, let us do the CSS file.

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

In here, is how we design what our website will look like. 

# JS

