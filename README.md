# Invoice OCR System

A CPU-optimized Optical Character Recognition (OCR) system for extracting key information from invoice images. This system uses advanced image preprocessing techniques and pattern matching to extract vendor names, total amounts, and dates from invoice receipts.

## Features

- **Advanced Image Preprocessing**: Multi-stage image enhancement including noise reduction, contrast enhancement, and adaptive thresholding
- **Multi-Configuration OCR**: Uses multiple Tesseract configurations to maximize text extraction accuracy
- **Intelligent Field Extraction**: Pattern-based extraction for vendor names, total amounts, and dates
- **Performance Evaluation**: Comprehensive accuracy metrics and evaluation against ground truth data
- **SROIE Dataset Support**: Built-in support for the SROIE (Scanned Receipt OCR and Information Extraction) dataset

## Installation

### Prerequisites

- Python 3.7+
- OpenCV
- Tesseract OCR engine

### Requirements.txt
```
opencv-python
pytesseract
numpy
pandas
pillow
scikit-learn
kagglehub
```
## System Architecture

### Image Preprocessing Pipeline

1. **Noise Reduction**: Using `cv2.fastNlMeansDenoising()`
2. **Contrast Enhancement**: CLAHE (Contrast Limited Adaptive Histogram Equalization)
3. **Gaussian Blur**: Smoothing for better text recognition
4. **Adaptive Thresholding**: Binary image conversion
5. **Morphological Operations**: Noise cleanup and text enhancement

### Field Extraction Patterns

The system uses regex patterns to extract:

- **Vendor Names**: Company names, store names, restaurant names
- **Total Amounts**: Various currency formats (USD, RM, etc.)
- **Dates**: Multiple date formats (DD/MM/YYYY, DD-MM-YYYY, etc.)

### OCR Configurations

Multiple Tesseract configurations are tested:
- `--oem 3 --psm 6 -l eng` (Default)
- `--oem 3 --psm 4 -l eng` (Single column)
- `--oem 3 --psm 3 -l eng` (Automatic)
- `--oem 1 --psm 6 -l eng` (Legacy engine)

## Performance

### Current Results (SROIE Dataset)

- **Overall Accuracy**: 11.11%
- **Vendor Name**: 0.00%
- **Total Amount**: 6.67%
- **Date**: 26.67%

### Performance Optimization

- CPU-optimized processing
- Memory-efficient image handling
- Batch processing support
- Configurable dataset limits

## File Structure

```
invoice-ocr-system/
├── invoice_ocr_system.py      # Main system implementation
├── requirements.txt           # Python dependencies
├── README.md                 # This file
├── examples/                 # Example usage scripts
│   ├── basic_usage.py
│   └── batch_processing.py
├── tests/                    # Unit tests
│   ├── test_preprocessing.py
│   ├── test_extraction.py
│   └── test_evaluation.py
└── results/                  # Output directory
    └── invoice_extraction_results.json
```

## API Reference

### InvoiceOCRSystem Class

#### Methods

- `__init__(dataset_path=None)`: Initialize the OCR system
- `load_dataset()`: Load and parse the SROIE dataset
- `process_invoices(image_paths)`: Process multiple invoice images
- `extract_text_with_ocr(image_path)`: Extract text from a single image
- `extract_fields_with_improved_patterns(text)`: Extract structured fields from text
- `evaluate_system(test_data, ground_truth)`: Evaluate system performance
- `save_results(results, output_file)`: Save results to JSON file

## Dataset Support

### SROIE Dataset

The system automatically downloads and processes the SROIE dataset:
- **Images**: 973 invoice/receipt images
- **Annotations**: Entity-level annotations for vendor, amount, and date
- **Format**: JSON-based annotation format



## Known Issues

- Low accuracy on handwritten invoices
- Challenges with rotated or skewed images
- Limited language support (English only)
- Performance varies with image quality
