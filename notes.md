# 26 REALISTIC RENDER 

## TONE MAPPING
- intends to convert High Dynamic Range (HDR) to Low Dynamic Range (LDR)
- fakes the process of converting LDR to HDR even if the colours aren't HDR resulting in a very realistic render 

### THREE.ReinhardToneMapping
- colours look washed out, but look realistic with a poorly set camera

## ANTIALIASING
- aliasing an artifact that might appear in some situations where you can see a stair-like effect
- usually on the edge of geometries 
- depends on pixel ratio
- when rendering of a pixel occurs, it tests what geometry is being rendered in that pixel and calculates the colour and puts it on the screen 

### SUPER SAMPLING (SSAA) OR FULLSCEEN SAMPING (FSAA)
- increase the resolution beyond actual one
- when resized to its normal size, each pixel colour is automatically averaged from the 4 pixels rendered
- easy but bad for performance (rendering 4x)

### MULTI SAMPLING (MSAA)
- automatically performed by recent GPUs
- will check neighbours of the pixel being rendered
- if at the edge of geometry it mixes colours with neighbours
- only works on geometry edges 
- screens with pixel ratio above 1 dont need it
- slightly exhausts resources

## SHADOWS
- environment maps can't cast shadows 
- need to add light that roughly matches lighting in the environment map and use it to cast the shadows
- default Three.js intensity values aren't realistic
    - based on arbitrary scale unit and don't reflect real world values
    - best to use realistic and standard values
- always start a project with `UseLegacyLights` to `false`

- Three.js uses matrices to define object transforms
- we you change proeprties like position, rotation, and scale those are compiled into a matrix
- this process is done right before the object is rendered and only if it's in the scene
    - can either add target to the scene or update the matrix manually using the `UpdateWorldMatrix()` method

## TEXTURES AND COLOUR SPACE
- textures look too white this is b/c of color space
- it's a way to optomise how colours are being stored according to the human eyes sensitivity
- mostly concerns textures that are supposed to be seen

### SHADOW ACNE
- can occur on both smooth and flat surfaces for precision reasons when calculating if the surface is in the shadow or not 
- the hamburger is casting a shadow on its own surface 