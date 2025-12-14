# Window Condensation & Comfort Calculator

[中文版 (Chinese Version)](README_CN.md)

An interactive calculator to visualize the relationship between indoor temperature, humidity, dew point, and living comfort.

- **Main File**: `index.html` (Single-file implementation for interaction, calculation, and visualization).
- **Assets**: Images are stored in `images/`.

## Quick Start (Development)
- Open `index.html` in your browser (double-click or use a local static server).

## Build for Production
To generate the protected, minified version of the application:

1.  **Install dependencies** (if you haven't already):
    ```bash
    npm install -g html-minifier
    ```

2.  **Run the build command**:
    ```bash
    # Create the docs directory (GitHub Pages supports /docs)
    mkdir -p docs

    # Minify HTML/CSS/JS
    npx html-minifier --collapse-whitespace --remove-comments --minify-js true --minify-css true -o docs/index.html index.html

    # Copy assets
    cp -r images docs/images
    ```

3.  **Deploy**: 
    *   Push your code to GitHub.
    *   Go to **Settings > Pages**.
    *   Select **Source**: `Deploy from a branch`.
    *   Select **Branch**: `main` (or your default branch) and **Folder**: `/docs`.

## Operation Guide

### 1. Adjust Environmental Parameters (Left Panel)
- **Indoor Temp**: Drag the slider to set the indoor temperature (15°C - 30°C).
- **Relative Humidity (RH)**: Set the saturation level of water vapor in the air (10% - 80%).
- **Lock AH (Absolute Humidity)**:
    - Click the "Lock AH" button to fix the actual water content in the air (g/m³).
    - **Use Case**: Simulates humidity changes when heating or cooling a sealed room. For example, if AH is locked at 8.0 g/m³, raising the temperature from 20°C to 25°C will automatically lower the relative humidity (air becomes drier).

### 2. Set External Conditions (Left & Right Panels)
- **Outdoor Temp**: Simulate weather from extreme cold (-40°C) to cool (15°C).
- **Window Type**: Select windows with different insulation properties in the "Window Simulation" card on the right:
    - `U=5.8` (Single Pane): Poor insulation, prone to condensation.
    - `U=2.8` (Standard Double Glazing): Standard configuration.
    - `U=1.6` / `U=0.8` (Low-E / Triple Glazing): High performance, resistant to condensation.

---

## Data Interpretation & Examples

The core of this tool is to demonstrate the balance between **Comfort** and **Physical Limits (Condensation)**.

### 1. Dew Point
> **Definition**: The temperature at which water vapor in the air begins to condense into liquid water.

*   **Example**:
    *   Settings: Indoor **22°C**, RH **50%**.
    *   Result: Dew Point is **11.1°C**.
    *   **Interpretation**: This means if the surface temperature of a window (or wall) is below 11.1°C, water vapor will condense into droplets on it.

### 2. Glass Surface Temp vs. Condensation Risk
Glass temperature depends on the indoor-outdoor temperature difference and the window's U-value (thermal conductivity).

*   **Scenario A: Condensation Crisis**
    *   **Conditions**: Outdoor **-10°C**, Indoor **22°C**, Humidity **50%** (Dew Point 11.1°C).
    *   **Window**: Single Pane (U=5.8).
    *   **Result**: Glass surface temp drops to **-0.4°C**.
    *   **Phenomenon**: -0.4°C < 11.1°C, and below freezing -> **Severe Icing/Frost**.

*   **Scenario B: Safe Balance**
    *   **Conditions**: Same as above (Outdoor -10°C, Indoor 22°C, Humidity 50%).
    *   **Window**: Standard Double Glazing (U=2.8).
    *   **Result**: Glass surface temp rises to **11.2°C**.
    *   **Phenomenon**: 11.2°C > 11.1°C -> **Glass Surface Dry** (Just avoided condensation).

### 3. Psychrometric Chart & Comfort Zones
The chart on the right shows whether the current air condition is suitable for living, based on the following standards:

#### A. Ideal Comfort Zone (Green Area)
The strictest standard for health and comfort, corresponding to "Perfect Comfort" in the status bar.
*   **Temperature Range**: 20°C - 25°C
*   **Humidity Range**: 40% - 60%
*   **Rationale**: Within this range, the human body feels most comfortable, and it effectively inhibits the spread of mold (>60% prone) and viruses (<40% active).

#### B. Acceptable Area (Amber Area)
A broader range that is tolerable for the human body.
*   **Temperature Range**: Approx. 15°C - 26°C
*   **Humidity Range**: Approx. 30% - 70% (Varies dynamically with temperature)
*   **Logic**:
    *   At low temps (e.g., 15°C), lower humidity is allowed because cold + damp feels worse.
    *   At high temps (e.g., 26°C), the upper humidity limit is lowered to avoid a "sauna" feeling.

#### C. Uncomfortable Zone (Blank Area)
*   **Too Dry (<40%)**: Prone to static electricity, dry skin, and respiratory discomfort.
*   **Too Humid (>60%)**: Prone to mold and dust mites, feeling stuffy or clammy.

---

## Future Improvements

### 1. Functionality Enhancements
*   **Presets**: Add one-click scenes like "Plum Rain Season" or "Northern Winter Night" to help users quickly understand typical climates.
*   **Custom U-Value**: Allow users to input specific window U-values to adapt to more building materials.
*   **Mold Risk Warning**: Add a mold growth risk index (usually occurs when surface humidity >80%).

### 2. User Experience
*   **Ventilation Simulation**: Add an "Open Window" button to dynamically calculate temperature and humidity changes after introducing outdoor air.
*   **Interactive Chart**: Support setting the state by directly clicking on the Psychrometric Chart.

### 3. Visuals & Immersion
*   **Dynamic Outdoor Background**: Automatically switch backgrounds based on outdoor temperature (e.g., snowy, rainy, sunny).
*   **Finer Particle Effects**: Use Canvas to simulate more realistic water droplet accumulation and flow effects.

### 4. Technical Architecture
*   **PWA Support**: Add offline support to allow installation as a standalone app.

---

## References

The calculation logic and comfort standards of this tool reference the following documents:

1.  **Psychrometrics - Dew Point and Wet-Bulb Temperature** (CED Engineering)
    *   [M08-011 - Course Preview - R1.pdf](https://www.cedengineering.com/userfiles/M08-011%20-%20Course%20Preview%20-%20R1.pdf)
2.  **Residential Indoor Air Quality Guideline: Moulds** (Health Canada)
    *   [H144-33-2016-eng.pdf](https://publications.gc.ca/collections/collection_2018/sc-hc/H144-33-2016-eng.pdf)

## License
- Copyright &copy; 2025 chefbig.ca. All Rights Reserved.
- This project is proprietary. Unauthorized copying, distribution, or modification is prohibited.
