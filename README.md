# SVG Path Template Image Replacer

A web-based tool for creating image templates with replaceable regions defined by SVG paths. Perfect for meme generators, product customizers, and dynamic content creation.

## Features

- Define non-rectangular, custom-shaped regions using SVG paths
- Replace regions with colors, gradients, or images
- Multiple fit modes: cover, contain, stretch
- Interactive region selection (click on canvas or dropdown)
- Export final compositions as PNG
- Visual path creation tool included

## Files

- `template-image-replacer.html` - Main application
- `svg-path-helper.html` - Tool for creating and editing SVG paths
- `template-example.json` - Example template configuration

## Quick Start

1. Open `template-image-replacer.html` in a web browser
2. Click on a region or select from the dropdown
3. Choose an asset to fill the region
4. Click "Export Final Image" to save

## Creating Custom Templates

### Template Structure

```javascript
const template = {
    width: 800,
    height: 600,
    backgroundImage: null,  // Optional: path to background image
    backgroundColor: '#f5f5f5',
    regions: [
        {
            id: 'unique_id',
            name: 'Display Name',
            path: 'M 100 100 L 200 100 L 150 200 Z',  // SVG path
            defaultFill: '#e0e0e0',
            allowedAssets: ['asset1', 'asset2'],
            fitMode: 'cover'  // 'cover', 'contain', or 'stretch'
        }
    ]
};
```

### Asset Types

```javascript
// Color
{
    name: 'Red',
    type: 'color',
    data: '#FF0000'
}

// Gradient
{
    name: 'Blue Gradient',
    type: 'gradient',
    data: {
        type: 'linear',
        colors: ['#0000FF', '#00FFFF']
    }
}

// Image
{
    name: 'Photo',
    type: 'image',
    data: 'path/to/image.jpg'
}
```

## Getting SVG Paths

### Method 1: Use the SVG Path Helper Tool
1. Open `svg-path-helper.html`
2. Click on the canvas to create points
3. Copy the generated path

### Method 2: From Design Software
1. Create shape in Inkscape, Illustrator, or Figma
2. Export as SVG
3. Open SVG file in text editor
4. Copy the `d` attribute from the `<path>` element

### Method 3: Online Tools
- Use online SVG editors
- Draw your shape
- Extract the path data

## SVG Path Syntax

- `M x y` - Move to point
- `L x y` - Line to point
- `Q x1 y1, x2 y2` - Quadratic curve
- `C x1 y1, x2 y2, x3 y3` - Cubic curve
- `Z` - Close path

Example:
```
M 100 100 L 200 100 L 150 200 Z
```
This creates a triangle.

## Fit Modes

- **cover** - Image fills entire region, may crop edges
- **contain** - Entire image fits within region, may have empty space
- **stretch** - Image stretches to fill region, may distort

## Advanced Usage

### Loading Templates from JSON

```javascript
fetch('template-example.json')
    .then(response => response.json())
    .then(data => {
        template = data;
        init();
    });
```

### Adding Background Images

```javascript
const template = {
    backgroundImage: 'background.jpg',
    // ... rest of template
};
```

### Dynamic Asset Loading

```javascript
const assetLibrary = {
    asset1: {
        name: 'User Upload',
        type: 'image',
        data: URL.createObjectURL(file)  // from file input
    }
};
```

## Browser Compatibility

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

Requires Canvas API and Path2D support.

## Examples

### Meme Template
```javascript
regions: [
    {
        id: 'topText',
        name: 'Top Text Area',
        path: 'M 50 50 L 750 50 L 750 150 L 50 150 Z',
        allowedAssets: ['text1', 'text2']
    },
    {
        id: 'image',
        name: 'Main Image',
        path: 'M 100 200 L 700 200 L 700 500 L 100 500 Z',
        allowedAssets: ['face1', 'face2', 'face3']
    }
]
```

### Product Customizer
```javascript
regions: [
    {
        id: 'logo',
        name: 'Logo Placement',
        path: 'M 350 250 Q 400 200, 450 250 Q 500 300, 450 350 Q 400 400, 350 350 Q 300 300, 350 250 Z',
        fitMode: 'contain',
        allowedAssets: ['logo1', 'logo2', 'logo3']
    }
]
```

## Tips

1. Use the path helper tool to visualize shapes before adding to template
2. Keep region IDs unique and descriptive
3. Test fit modes with different aspect ratio images
4. Use contain mode for logos, cover mode for backgrounds
5. Define reasonable bounds for paths to avoid performance issues

## License

Free to use for any purpose.
