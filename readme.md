## Minecraft Block Renderer in JavaScript
#### Made by [Chaos](http://static.chaofan.io/blockRenderer/), Modified by FlamingoBike#6228 & Forked by Eluinn

---

## Description

This tool allows you to render custom minecraft blocks to 512x512 images (size customizable by modifying `index.html`).

---

## How to Use

- Serve the `index.html` page on a local web server (the easiest way to do this is to open the project with Visual Studio Code, and use the `Live Server` extension).
    -*note: Live Server will only work on local files. You must download the repository to use it this way*
- Select a model from the dropdown menu.
- Select textures for the top, left, and right faces from the dropdown menus, or upload your own texture.
- Click Save File when you are ready, and it will download a png of what you have created.

---

## Models

- It is very easy to add new models. Simply navigate to the `models` folder in the minecraft assets (accessible by opening any version's jar with something like 7zip), and look at the .json file of the model you wish to replicate. Then, go over to the `blockModel.js` file and create a new variable in the `models` variable (line 114). You can add cubes and planes according to the json model by looking at the coordinate vectors `from` and `to` (keep in mind they are in pixels, so you have to divide the values by 16).
    - For example: part of the stairs_stone model from LBPR *(note:the original model has many more lines)*
    ```
    "elements": [
        {   "__comment": "Main Plate",
			"from": [ 8, 0, 0 ],
            "to": [ 16, 6.75, 16 ],
            "faces": {
                "down":  { "texture": "#bottom", "cullface": "down" },
                "up":  	 { "texture": "#top" },
                "north": { "texture": "#side", "cullface": "north" },
                "south": { "texture": "#side", "cullface": "south" },
                "east":  { "texture": "#side", "cullface": "east" }
            }
        },
		
		
		
		{  "__comment": "Layer1 Plate1",
			"from": [ 0, 0, 0 ],
            "to": [ 8, 2.125, 16 ],
            "faces": {
                "down":  { "texture": "#bottom", "cullface": "down" },
                "up":    { "texture": "#top" },
                "north": { "texture": "#side", "cullface": "north" },
                "south": { "texture": "#side", "cullface": "south" },
                "west":  { "texture": "#side", "cullface": "west" }
            }
        },
        ```
    - You would determine the name for your model, I like to use the pack name and original model name so I can find it if necessary. I also add comments to make it easier to keep track, but it is not required. Your new code would be the following
    ```
    var lbpr_stairs_stone = new Model();
	//Main Plate
	lbpr_stairs_stone.addCube(8/16, 0, 0, 16/16, 6.75/16, 16/16);
	//Layer1 Plate1
	lbpr_stairs_stone.addCube(0, 0, 0, 8/16, 2.125/16, 16/16);
    ```
    - Then add the following to the return section, below var models
    ```
    "lbpr_stairs_stone" : lbpr_stairs_stone
    ```
- Once you're done, invert the x and z to rotate it like it is in game (at least, I've had to do this for the fence and wall inventory models).

## Textures

- You can add more textures without uploading them, by placing them in the `presets` folder. Then, open that folder in a terminal, and run `ls` to get a list of all the files, and copy said list in the `presets.js` file, to make them actually show up in the texture dropdown selects.

## Other Notes

- If you added a new model and you wish to append its name to the downloaded file (for example, fences, walls, slabs, and stairs block names always specify what they are, like `stone_slab`, `oak_fence`, etc...), you can add it to the hardcoded whitelist in the `shouldAddModelNameToFile()` function, in `index.html`.
- Play around with it! It was very fun to get into the various details, I'm sure it's also quite simple to add shaders to have more than just cubes and planes.
