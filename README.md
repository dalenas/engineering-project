# Engineering Project - Foundation Mixture Creator

## Software Requirements (Abridged)
1. Pi Camera → capture frame (locked exposure/WB if you can).
2. OpenCV → face detection → skin mask → robust skin color (median).
3. Convert to Lab → compare with skin shade DB in Lab.
4. k-NN (k=3 or 5) → pick closest brand shade + compute ΔE
5. Map that shade to real pigment recipe (a small lookup table you define).
6. Convert pigment volumes → servo turns → push syringes via leadscrews.
7. Show on-screen: target shade, chosen shade, ΔE, and per-pigment ratios

### Open-source skin-shade / Lab

* Numerical RGB and LAB values of skin colors for Cabinet members of 32 countries([University Digital Conservancy][1])
* ENCoDE Skin Color Dataset ([PhysioNet][2])
* Monk Skin Tone Scale (MST)([Wikipedia][3])
* Training and Testing Datasets ([Zenodo][4])
* Skin Tone Classification Dataset on Kaggle ([Kaggle][5])
  * Ensure the values have a known white point.
  * Convert RGB → Lab if needed : lin transform

[1]: https://conservancy.umn.edu/items/3308e188-d048-4d31-a203-1329d5cf1c6d?utm_source=chatgpt.com "Numerical RGB and LAB values of skin colors for Cabinet ..."
[2]: https://physionet.org/content/encode-skin-color/?utm_source=chatgpt.com "ENCoDE, mEasuring skiN Color to correct pulse Oximetry ..."
[3]: https://en.wikipedia.org/wiki/Monk_Skin_Tone_Scale?utm_source=chatgpt.com "Monk Skin Tone Scale"
[4]: https://zenodo.org/records/5532176?utm_source=chatgpt.com "Training and Testing Datasets for skin colour characterisation"
[5]: https://www.kaggle.com/datasets/usamarana/skin-tone-classification-dataset?utm_source=chatgpt.com "Skin Tone Classification Dataset"

### Pigment Mapping Table

1. Select a subset of “anchor shades” (idk what number is good i feel like we want a wide variety but not too many) from your skin‐shade database that you want to support directly.
2. For each anchor shade, measure the pigment ratio that you believe will mix to that shade.
3. Store the table: something like this not precise

   ```
   name, L, A, B, Blue_ratio, Yellow_ratio, Red_ratio...
   Medium-Tan, 55.1, 10.2, 14.3, 0.30, 0.40, 0.30...
   ```
4. At runtime:
   * Use your k-NN to pick the closest anchor shade.
   * Or interpolate between anchors if target falls in between (e.g., weighted by inverse distance).
