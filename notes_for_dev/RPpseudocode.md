# 2: Raspberry Pi Code

```python
def EVENT_HANDLER():
    #extract lab values
    SAMPLE_PICTURE = CAMERA_CAPUTRE initiated by BUTTON_PRESS
    LAB_VALUES = IMAGE_PROCESSING(SAMPLE_PICTURE)
    
    #K nearest neighbor algo to find recipe
    SKIN_SHADE_TABLE = load("FOUNDATION_SHADE_RECIPE_DATBASE.csv")
    TARGET_SHADE = find closest shade via k-Nearest-Neighbor algorithm with LAB_VALUES
    
    #calculate servo turns for desired recipe
    PAINT_QUANTITIES =  assign paint quantities indicating how many 
                        times the servo should turn with TARGET_SHADE
    
    DEPLOY_TO_RASPBERRY_PI(PAINT_QUANTITIES)
    #servo motors move syringes
```