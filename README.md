The original version of **pdfsandwich** is available at [http://www.tobias-elze.de/pdfsandwich/](http://www.tobias-elze.de/pdfsandwich/); all credit for the initial development belongs to the original creator.

This fork maintains the core functionality of **pdfsandwich 0.1.7** but introduces a specific optimization for processing efficiency. It utilizes the ImageMagick `identify` command to calculate the entropy of each page:

`identify -format "%[entropy]" inputfile`

To invoke the new flag just call: `pdfsandwich -max_entropy 0.5 inputfile`


### Key Features and Changes
* **Entropy-Based Filtering:** The tool now evaluates every page to determine whether it should be processed or skipped.
* **New Parameter (`-max_entropy`):** Users can define a threshold between `0.0` and `1.0`. 
* **Performance Optimization:** If a page's entropy exceeds the specified threshold, OCR is skipped for that page. This prevents Tesseract from stalling on high-entropy pages (such as complex images or noise), which typically require significant computation time.

This modification was specifically designed for integration with [open-ocr](https://github.com/xf0e/open-ocr).
