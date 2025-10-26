# 1: Color Bias Adjustment and Sampling
```python
def IMAGE_PROCESSING(sample_picture) :
    #INPUT: sample_picture - image captured by camera
    #OUTPUT: LAB_values - color values compatible with paint mixing

    ### Get/Validate image containing skin region 
    ### & reference colors/control sheet

    if sample_picture is EMPTY/NOT_DETECTED :
        RAISE_ERROR "Image captured failed or canceled"
        return NULL

    SKIN_SAMPLE = list of pixel values that constitute a skin region
        ### INPUT: sample_picture
    CONTROL_SAMPLE = list of pixels that encompass the reference color sheet
        ### INPUT: sample_picture

    if control is EMPTY/NOT_DETECTED :
        RAISE_ERROR "Image does not contain control set. Retake picture with printout."
        return NULL
    

    # take rgb code of skin & the reference colors

    RGB_SKIN_RAW = calculated average of SKIN_SAMPLE
    CONTROL_MEASURED_VALUES = calculated average of CONTROL_SAMPLE

    # find difference in the read reference vs the known values on the sheet

    CONTROL_KNOWN_VALUES = load "CONTROL_DATABASE.csv"
    DIFFERENCE = calculate offset between CONTROL_MEASURED_VALUES and CONTROL_KNOWN_VALUES
    CCM_MATRIX = generate color correction matrix with DIFFERENCE

    # apply difference to the values found in the skin region for lighting correction

    RGB_SKIN_CORRECTED = apply CCM_MATRIX to RGB_SKIN_RAW

    # convert rgb value to lab for later processing

    LAB_VALUES = convert RGB_SKIN_CORRECTED to LAB(XYZ)

    for element in LAB_VALUES :
        if element is OUT_OF_RANGE :
            RAISE_ERROR "color conversion error. take a new picture." 
            return NULL

    return LAB_VALUES

def DETECT_SKIN_REGION(sample_picture) -> np.ndarray 
    


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