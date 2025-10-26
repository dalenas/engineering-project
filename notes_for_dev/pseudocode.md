# 1: Color Bias Adjustment and Sampling
```python
def IMAGE_PROCESSING(sample_picture) :
    #OUTPUT: LAB_values

    # Get image containing skin region & reference colors/control sheet

    if sample_picture is None :
        RAISE_ERROR "Image captured failed or canceled"
        return None

    skin = DETECT_SKIN_REGION(sample_picture)
    control = DETECT_REFERENCE_PATCHES(sample_picture)

    if control is None :
        RAISE_ERROR "Image does not contain control set. Retake picture with printout."
        return None
    

    # take rgb code of skin & the reference colors

    rgb_skin_raw = AVG_RGB(sample_picture, skin)
    rgb_control_reading = AVG_RGB(sample_picture, control)

    # find difference in the read reference vs the known values on the sheet

    rgb_control_known = LOAD_REFERENCE('control_table.csv')
    delta_E = CALCULATE_DIFFERENCE(rgb_control_known, rgb_control_reading)
    ccm_matrix = GENERATE_CCM(delta_E)

    # apply difference to the values found in the skin region for lighting correction

    rgb_skin_corrected = APPLY_CCM(ccm_matrix, rgb_skin_raw)

    # convert rgb value to lab for later processing

    LAB_values = CONVERT_RGB_LAB(rgb_skin_corrected)

    for element in LAB_values :
        if element is OUT_OF_RANGE :
            RAISE_ERROR "color conversion error. take a new picture." 
            return None

    return LAB_values

def DETECT_SKIN_REGION(sample_picture) -> np.ndarray 
    # OUTPUT: skin mask that highlights regions of skin to evaluate
    # the "mask" is a map of pixels that belong to a region 


def DETECT_REFERENCE_PATCHES(sample_picture) -> np.ndarray
    # OUTPUT: control mask that highlights the printout that has reference colorsx
    
def AVG_RGB(sample_picture, region) -> list
    # OUTPUT: rgb_list #[r, g, b]
    # computes average RGB of the defined skin regions

def CALCULATE_DIFFERENCE(rgb_control_known, rgb_control_reading) -> list
    # OUTPUT: delta_E #[r, g, b] of the offset

def GENERATE_CCM(delta_E) -> list[list]
    # OUTPUT: ccm_matrix #2d list -> 3x3 matrix correcting the offset
    # uses the offset between expected rgb of control set and measured value (delta_E)
    # to construct matrix that can be applied to rgb of skin sample

def APPLY_CCM(ccm_matrix, rgb_skin_raw) -> list
    # OUTPUT: rgb_skin_corrected
    #runs skin sample through generated color corrector

def CONVERT_RGB_LAB(rgb_skin_corrected) -> list
    # OUTPUT: LAB_values
    # Utilizes a linear transformation that converts rgb to LAB
    # openCV has a function that does this


```