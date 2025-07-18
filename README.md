# Image Authentication Checker

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-yellow.svg)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)

A comprehensive web-based tool for digital image forensic analysis and authenticity verification. This application provides advanced forensic techniques to detect image tampering, manipulation, and editing through multiple analysis methods.

## 🚀 Features

### Core Analysis Methods

- **Error Level Analysis (ELA)** - Real recompression-based tampering detection
- **Noise Pattern Analysis** - Consistency analysis across image regions
- **Metadata Verification** - EXIF data extraction and inconsistency detection
- **Compression Analysis** - JPEG artifact and quality inconsistency detection

### User Experience

- **Client-Side Processing** - All analysis performed locally, no server uploads
- **Real-Time Progress** - Accurate progress tracking for each analysis step
- **Interactive Results** - Visual overlays and detailed scoring
- **Export Capabilities** - JSON, TXT, HTML, and PDF report generation
- **Responsive Design** - Works on desktop, tablet, and mobile devices

## 🚀 Installation & Setup

### Option 1: Direct Usage (Recommended)
1. Download or clone this repository
2. Open `index.html` in a modern web browser
3. No additional setup required - all dependencies are loaded via CDN

### Option 2: Local Development
```bash
git clone https://github.com/your-username/image-authentication-checker.git
cd image-authentication-checker
# Open index.html in your preferred browser
```

### System Requirements
- Modern web browser with JavaScript enabled
- Minimum 4GB RAM for large image processing
- Internet connection for CDN dependencies (first load only)

## 📋 Quick Start

1. **Upload Image**: Choose or drag & drop an image file (JPEG, PNG, TIFF, WebP)
2. **Configure Analysis**: Select which forensic methods to apply
3. **Adjust Settings**: Optionally configure ELA quality and other parameters
4. **Run Analysis**: Click "Start Comprehensive Analysis"
5. **View Results**: Get comprehensive authenticity assessment with visual indicators
6. **Export Report**: Generate PDF, HTML, JSON, or TXT reports

## 💡 Usage Examples

### Example 1: Basic Authenticity Check
```
1. Upload a suspicious image
2. Keep all analysis methods enabled (default)
3. Click "Start Comprehensive Analysis"
4. Review the overall authenticity score
5. Examine individual analysis results
```

### Example 2: Advanced ELA Analysis
```
1. Upload image
2. Click "ELA Settings" to expand advanced options
3. Adjust compression quality (try 70%, 80%, 90%)
4. Enable only "ELA Analysis"
5. Compare results at different quality levels
```

### Example 3: Metadata Investigation
```
1. Upload image with suspected metadata tampering
2. Enable only "Metadata Check"
3. Review EXIF data table for inconsistencies
4. Look for editing software signatures
5. Check date/time consistency
```

### Example 4: Batch Analysis Workflow
```
1. Analyze multiple images from the same source
2. Compare noise patterns across images
3. Look for consistency in metadata
4. Document findings in exported reports
```

## 🔬 Technical Implementation

### Error Level Analysis (ELA)

**How it works:**
- Recompresses the image at a specified JPEG quality level (default: 90%)
- Calculates pixel-by-pixel differences between original and recompressed versions
- Amplifies differences for visualization (8x amplification factor)
- Highlights areas with compression inconsistencies

**Technical Details:**
```javascript
// Core ELA algorithm
const errorLevel = (rDiff + gDiff + bDiff) / 3;
const amplifiedError = Math.min(errorLevel * 8, 255);
```

**Scoring Algorithm:**
- Base score: 100 points
- Penalty for high average error: up to -50 points
- Penalty for high variance: up to -30 points  
- Penalty for many high-error pixels: up to -20 points

**Interpretation:**
- **Bright areas** in ELA image indicate potential tampering
- **Consistent gray** suggests authentic regions
- **Sharp boundaries** may indicate splicing or copy-paste operations

### Noise Pattern Analysis

**How it works:**
- Divides image into 8x8 pixel blocks
- Calculates noise variance within each block
- Compares noise patterns across the entire image
- Identifies regions with inconsistent noise characteristics

**Technical Details:**
```javascript
// Noise calculation per block
const blockNoise = calculateBlockNoise(data, x, y, blockSize, width);
const avgNoise = noiseVariance / blockCount;
const noiseStdDev = Math.sqrt(calculateVariance(noiseValues));
```

**Forensic Significance:**
- **Consistent noise** indicates single capture source
- **Noise discontinuities** suggest splicing or compositing
- **Unnatural smoothness** may indicate heavy editing or AI generation

### Metadata Verification

**How it works:**
- Extracts EXIF data using EXIF.js library
- Maps technical tags to human-readable format
- Analyzes date consistency, software traces, and GPS data
- Detects common editing software signatures

**Key Metadata Fields:**
- Camera make/model and settings (ISO, aperture, focal length)
- Creation, modification, and digitization timestamps
- Software used for processing
- GPS coordinates and orientation data
- Color space and compression information

**Red Flags:**
- Mismatched creation/modification dates
- Missing EXIF data (possible stripping)
- Editing software signatures (Photoshop, GIMP, etc.)
- Inconsistent camera settings for lighting conditions

### Compression Analysis

**How it works:**
- Analyzes 8x8 JPEG compression blocks
- Detects compression artifacts and block boundaries
- Identifies multiple compression generations
- Calculates artifact density and strength

**Technical Implementation:**
```javascript
// Compression artifact detection
const artifactStrength = detectCompressionArtifact(data, x, y, blockSize, width);
const artifactRatio = artifactCount / totalBlocks;
```

**Forensic Indicators:**
- **High artifact density** suggests multiple compressions
- **Block boundary visibility** indicates JPEG processing
- **Quality inconsistencies** may reveal edited regions

## 📊 Interpreting Results

### Overall Authenticity Score

| Score Range | Interpretation | Confidence Level |
|-------------|----------------|------------------|
| 80-100 | Likely Authentic | High |
| 60-79 | Uncertain/Suspicious | Medium |
| 0-59 | Highly Suspicious | High |

### Analysis-Specific Indicators

**ELA Analysis:**
- Score > 70: Low tampering signs
- Score 40-70: Moderate concern
- Score < 40: High tampering signs

**Noise Analysis:**
- Score > 70: Consistent noise patterns
- Score 40-70: Some irregularities detected
- Score < 40: Inconsistent noise (possible splicing)

**Metadata Analysis:**
- Score > 80: No critical issues
- Score 60-80: Minor warnings present
- Score < 60: Critical inconsistencies found

**Compression Analysis:**
- Score > 70: Low compression artifacts
- Score 40-70: Moderate artifacts
- Score < 40: High artifacts (multiple compressions)

## 🔍 Forensic Best Practices

### Image Collection
- Obtain images in original format when possible
- Document chain of custody
- Preserve original file timestamps and metadata
- Avoid unnecessary format conversions

### Analysis Workflow
1. **Initial Assessment** - Check file format, size, and basic metadata
2. **Metadata Analysis** - Examine EXIF data for inconsistencies
3. **Visual Inspection** - Look for obvious signs of manipulation
4. **Technical Analysis** - Apply ELA, noise, and compression analysis
5. **Cross-Validation** - Compare results across multiple methods
6. **Documentation** - Generate comprehensive reports

### Limitations and Considerations
- **False Positives** - Heavy compression or processing can trigger alerts
- **False Negatives** - Sophisticated editing may not be detected
- **Format Dependencies** - Some methods work better with JPEG images
- **Quality Factors** - Low-resolution images may produce unreliable results

### Expert Recommendations
- **Multi-Method Approach**: Never rely on a single analysis method
- **Source Context**: Consider image source and acquisition method
- **Processing History**: Account for legitimate processing (camera software, social media compression)
- **Visual Correlation**: Combine technical analysis with visual examination
- **Evidence Corroboration**: Seek corroborating evidence when possible
- **Quality Assessment**: Higher resolution images provide more reliable results
- **Format Considerations**: JPEG images work best for compression-based analysis
- **Baseline Comparison**: Compare with known authentic images from same source when available

### Common False Positive Scenarios
- **Heavy JPEG Compression**: May trigger ELA and compression analysis alerts
- **Social Media Processing**: Automatic filters and compression can appear suspicious
- **Camera Processing**: In-camera HDR, noise reduction, and sharpening
- **Format Conversion**: Converting between formats can introduce artifacts
- **Legitimate Editing**: Basic adjustments (brightness, contrast) may show in analysis
- **Low Quality Images**: Poor resolution can produce unreliable analysis results

### Common False Negative Scenarios
- **Professional Editing**: Sophisticated manipulation may not be detected
- **AI-Generated Content**: Advanced AI may produce convincing fake images
- **Subtle Manipulations**: Minor edits may fall below detection thresholds
- **Format Limitations**: Some manipulations are harder to detect in certain formats
- **High-Quality Forgeries**: Professional-grade editing with careful attention to artifacts

## 🛠️ Development Roadmap

### Current Limitations & Improvements Needed

**Error Level Analysis:**
- [ ] Multiple quality level testing (70%, 80%, 90%, 95%)
- [ ] Advanced recompression algorithms
- [ ] Better handling of PNG and TIFF formats
- [ ] Automatic quality detection

**Noise Pattern Analysis:**
- [ ] Advanced statistical noise models
- [ ] Machine learning-based noise classification
- [ ] Support for different sensor noise patterns
- [ ] Improved block size optimization

**Metadata Analysis:**
- [ ] Support for more camera manufacturers
- [ ] Advanced timestamp correlation analysis
- [ ] Thumbnail extraction and comparison
- [ ] GPS coordinate validation

**Compression Analysis:**
- [ ] DCT coefficient analysis
- [ ] Quantization table examination
- [ ] Multi-generation compression detection
- [ ] Format-specific artifact detection

### Planned Features

**Short Term (v2.0):**
- [ ] Batch processing capabilities
- [ ] Advanced ELA quality settings
- [ ] Improved mobile responsiveness
- [ ] Enhanced report templates

**Medium Term (v3.0):**
- [ ] Copy-Move detection algorithm
- [ ] Splicing detection using texture analysis
- [ ] AI-generated image detection
- [ ] Advanced statistical analysis

**Long Term (v4.0):**
- [ ] Machine learning integration
- [ ] Blockchain verification support
- [ ] Advanced visualization tools
- [ ] Professional forensic reporting

## 📁 Project Structure

```
image-authentication-checker/
├── index.html              # Main application file
├── README.md               # This documentation
└── init-reqs.md            # Initial requirements
```

## 🔧 Dependencies

- **EXIF.js** - EXIF metadata extraction
- **jsPDF** - PDF report generation
- **Font Awesome** - Icons and UI elements
- **Tailwind CSS** - Styling framework

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

## 🔧 Troubleshooting

### Common Issues

**Issue: "EXIF library not loaded" error**
- **Cause**: Network connectivity issues or CDN unavailability
- **Solution**: Refresh the page or check internet connection
- **Workaround**: Download EXIF.js locally and update the script src

**Issue: Analysis fails with large images**
- **Cause**: Browser memory limitations
- **Solution**: Resize image to under 4000x4000 pixels
- **Alternative**: Use a desktop browser with more available memory

**Issue: ELA analysis shows no results**
- **Cause**: Image format not suitable for recompression
- **Solution**: Convert to JPEG format before analysis
- **Note**: PNG and TIFF images may not show ELA results

**Issue: Progress bar stuck at certain percentage**
- **Cause**: JavaScript error during analysis
- **Solution**: Open browser console (F12) to check for errors
- **Workaround**: Refresh page and try with different image

**Issue: Metadata analysis shows "No EXIF data found"**
- **Cause**: Image has been processed or EXIF data stripped
- **Explanation**: This is normal for social media images or edited photos
- **Note**: Absence of EXIF data can itself be forensically significant

### Performance Optimization

**For Large Images:**
- Resize to maximum 2000x2000 pixels for faster processing
- Close other browser tabs to free memory
- Use Chrome or Firefox for better performance

**For Batch Analysis:**
- Process images one at a time
- Clear browser cache between sessions
- Monitor system memory usage

### Browser Compatibility

**Fully Supported:**
- Chrome 80+, Firefox 75+, Safari 13+, Edge 80+

**Limited Support:**
- Internet Explorer: Not supported
- Older mobile browsers: May have memory limitations

**Required Features:**
- Canvas API, File API, ES6+ JavaScript support

## 📞 Support

If you encounter any issues or have questions about the forensic analysis results, please:

1. Check the troubleshooting section above
2. Review the browser console for error messages
3. Open an issue on GitHub with:
   - Browser version and operating system
   - Image format and approximate size
   - Error messages or unexpected behavior
   - Steps to reproduce the issue

## 🧪 Advanced Technical Details

### Algorithm Implementation Details

**Error Level Analysis Implementation:**
```javascript
function calculateELADifferences(originalData, recompressedData) {
    const data = originalData.data;
    const recompData = recompressedData.data;
    const resultData = new Uint8ClampedArray(data.length);

    for (let i = 0; i < data.length; i += 4) {
        // Calculate absolute differences for each channel
        const rDiff = Math.abs(data[i] - recompData[i]);
        const gDiff = Math.abs(data[i + 1] - recompData[i + 1]);
        const bDiff = Math.abs(data[i + 2] - recompData[i + 2]);

        // Calculate combined error level
        const errorLevel = (rDiff + gDiff + bDiff) / 3;

        // Amplify the error for visualization
        const amplifiedError = Math.min(errorLevel * 8, 255);

        // Set result pixel (grayscale representation)
        resultData[i] = amplifiedError;     // R
        resultData[i + 1] = amplifiedError; // G
        resultData[i + 2] = amplifiedError; // B
        resultData[i + 3] = 255;            // A
    }

    return new ImageData(resultData, originalData.width, originalData.height);
}
```

**Noise Analysis Block Processing:**
```javascript
function calculateBlockNoise(data, x, y, blockSize, width) {
    let noise = 0;
    for (let by = 0; by < blockSize; by++) {
        for (let bx = 0; bx < blockSize; bx++) {
            const idx = ((y + by) * width + (x + bx)) * 4;
            if (idx < data.length - 2) {
                const r = data[idx];
                const g = data[idx + 1];
                const b = data[idx + 2];
                // Calculate color channel differences as noise indicator
                noise += Math.abs(r - g) + Math.abs(g - b) + Math.abs(b - r);
            }
        }
    }
    return noise / (blockSize * blockSize);
}
```

### Performance Considerations

**Memory Usage:**
- Original image data: W × H × 4 bytes (RGBA)
- Recompressed image data: W × H × 4 bytes
- ELA result data: W × H × 4 bytes
- Peak memory usage: ~3× original image size

**Processing Time:**
- ELA Analysis: O(W × H) - linear with pixel count
- Noise Analysis: O((W/8) × (H/8)) - depends on block size
- Metadata Analysis: O(1) - constant time
- Compression Analysis: O((W/8) × (H/8)) - block-based processing

**Browser Compatibility:**
- Chrome 60+, Firefox 55+, Safari 12+, Edge 79+
- Requires Canvas API and File API support
- WebGL not required but beneficial for large images

### Security Considerations

**Client-Side Processing Benefits:**
- No image data transmitted to servers
- Complete privacy protection
- No storage of sensitive images
- Immediate processing without network delays

**Potential Limitations:**
- Limited by browser memory constraints
- No server-side validation of results
- Dependent on client-side JavaScript execution
- Potential for code inspection/modification

## 📚 Research References

### Academic Papers
1. Krawetz, N. (2007). "A Picture's Worth: Digital Image Analysis and Forensics"
2. Farid, H. (2009). "Image forgery detection: A survey"
3. Popescu, A. C., & Farid, H. (2005). "Exposing digital forgeries by detecting traces of resampling"
4. Luo, W., Qu, Z., Pan, F., & Huang, J. (2007). "A survey of passive technology for digital image forensics"

### Technical Standards
- ISO/IEC 23008-12:2017 - Image File Format
- JPEG Standard (ISO/IEC 10918)
- EXIF 2.32 Specification
- TIFF 6.0 Specification

### Forensic Methodologies
- NIST Guidelines for Digital Forensics
- ACPO Good Practice Guide for Digital Evidence
- ISO/IEC 27037:2012 - Digital Evidence Guidelines

## ⚠️ Disclaimer

This tool is designed for educational and research purposes. While it implements established forensic techniques, results should be interpreted by qualified digital forensic experts. The tool should not be used as the sole basis for legal or investigative conclusions.

**Important Notes:**
- Results may vary based on image quality and format
- False positives can occur with heavily processed legitimate images
- Professional forensic analysis requires multiple validation methods
- Legal admissibility depends on jurisdiction and case requirements
