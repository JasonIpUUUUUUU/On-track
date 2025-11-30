# Times Square Hong Kong - Photo Location Estimator 📍

An AI-powered tool that analyzes photos taken inside Times Square mall (Hong Kong) and estimates the exact position where each photo was taken, displaying results on a floor plan with directional indicators.

## Features

- 🤖 **AI Vision Analysis**: Uses GPT-4 Vision to detect shop names, facilities, and architectural features
- 🗺️ **Position Triangulation**: Estimates location based on visible landmarks and their known positions
- 🧭 **Direction Detection**: Determines which way the camera is facing
- 📊 **Confidence Scoring**: Provides confidence levels for each estimate
- 🖼️ **Visual Output**: Generates annotated floor plans with position markers

## How It Works

1. **Photo Analysis**: Each photo is analyzed by AI to detect:
   - Visible shop/brand names (Lane Crawford, Gucci, Dior, etc.)
   - Floor level (based on ceiling, architecture, visible floors)
   - Facilities (escalators, elevators, toilets)
   - Spatial layout (what's on left, center, right)

2. **Position Estimation**: Using detected landmarks:
   - Matches visible shops to known floor plan positions
   - Triangulates position based on multiple reference points
   - Estimates direction based on shop arrangement

3. **Visualization**: Outputs a floor plan with:
   - 🔴 Red circle: Estimated position
   - 🔺 Red triangle: Direction camera is facing
   - ⭕ Outer ring: Confidence range (larger = less certain)

## Installation

```bash
cd /Users/JIP/Desktop/Orbis
pip install -r requirements.txt
```

## Usage

### With OpenAI API (Recommended)
```bash
export OPENAI_API_KEY="your-api-key-here"
python mall_locator.py
```

### Without API (Fallback Mode)
The program includes fallback analysis for the sample photos:
```bash
python mall_locator.py
```

## Output

Results are saved in the `output/` folder:
- `location_*.png` - Individual annotated floor plans for each photo
- `combined_*.png` - Combined view showing all positions on each floor
- `location_results.json` - Detailed analysis results

## Sample Photos Analysis

Based on the photos in `TimesSquarePhotos/`:

| Photo | Floor | Visible Landmarks | Direction |
|-------|-------|-------------------|-----------|
| 15.41.24 | GF | Lane Crawford, Celine, Chanel, Bottega Veneta | NE (facing escalators) |
| 15.41.46 | B1 | Fortress | N (on escalator) |
| 15.42.05 | GF | Lane Crawford, Gucci, Dior | N (central walkway) |
| 15.43.02 | B2 | Shake Shack, The Body Shop | N (near lifts) |

## Floor Data

The program includes data for Times Square HK floors:
- **B2**: Basement 2 - Food court, Shake Shack, The Body Shop
- **B1**: Basement 1 - Electronics (Fortress)
- **GF**: Ground Floor - Luxury brands (Lane Crawford, Gucci, Dior, Chanel)
- **1F-2F**: Fashion and Beauty zones
- **7F-13F**: Dining and Cinema

## Customization

### Adding More Shop Positions
Edit `SHOP_POSITIONS` in `mall_locator.py`:
```python
SHOP_POSITIONS = {
    "Shop Name": {"floor": "GF", "x": 0.5, "y": 0.5, "area": "central"},
    # x, y are normalized 0-1 coordinates on the floor plan
}
```

### Using Real Floor Plans
Replace the generated floor plans with actual images from the mall:
1. Download floor plans from https://timessquare.com.hk/floor-plan/
2. Save them in `floor_plans/` as `GF.png`, `B1.png`, etc.
3. Update the `create_floor_plan_image()` function to load these images

## Technical Details

- **AI Model**: OpenAI GPT-4 Vision (gpt-4o)
- **Position Algorithm**: Centroid-based triangulation with directional adjustment
- **Coordinate System**: Normalized (0-1) coordinates for floor-agnostic positioning

## References

- [Times Square Hong Kong Floor Plan](https://timessquare.com.hk/floor-plan/)
- Mall Address: 1 Matheson Street, Causeway Bay, Hong Kong

## License

MIT License - Feel free to modify and use!

