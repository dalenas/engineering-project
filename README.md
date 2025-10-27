# Engineering Project - Foundation Mixture Creator
## Before PM4
1. set up environment
2. pick skin color database and figure out how we will define the pigment matching table
3. discover tools needed (OpenCV)
4. develop detailed pseudocode


---

## Software Requirements (Abridged)
1. Pi Camera → capture frame 
2. OpenCV → face detection → skin mask → robust skin color
3. Convert RGB to XYZ -> removes camera bias (gamma to normal RGB to XYZ)
4. Convert to Lab → compare with skin shade DB in Lab. 
5. Convert pigment volumes → servo turns → push syringes via leadscrews.
6. Show on-screen: target shade, chosen shade, other options for shades (cooler tone/warmer tone. this is optional though)


### Pigment Mapping Table

1. Select a subset of “anchor shades” (idk what number is good i feel like we want a wide variety but not too many) from your skin‐shade database that you want to support directly.
2. For each anchor shade, measure the pigment ratio that you believe will mix to that shade.
3. Store the table: something like this not precise

   ```
   name, L, A, B, Blue_ratio, Yellow_ratio, Red_ratio...
   Medium-Tan, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0...
   ```
