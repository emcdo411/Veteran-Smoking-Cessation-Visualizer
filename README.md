### New README for `Veteran-Smoking-Cessation-Visualizer`

```markdown
# Veteran-Smoking-Cessation-Visualizer

Welcome to **`Veteran-Smoking-Cessation-Visualizer`**! This project explores smoking prevalence among older veterans (ages 50-70) using simulated data, visualized with advanced tools in Python and RStudio. Designed as part of my data science journey, it maps potential veteran living locations near Southern Illinois University-Carbondale (SIU-C) with smoking cessation insights—perfect for health policy analysis or a tech portfolio!

## Project Overview
- **Goal**: Visualize smoking prevalence by age range and link it to fictional veteran communities in Southern Illinois.
- **Tools**: Python (`pandas`) for data creation, RStudio (`ggplot2`, `leaflet`, `plotly`) for visualizations.
- **Data**: Simulated, with cities/zip codes near SIU-Carbondale added.

## Files
- `create_smoking_cessation_analysis_extended.py`: Python script to generate the `.csv`.
- `smoking_cessation_analysis_extended.csv`: Simulated dataset (generated, not stored in repo).
- `smoking_prevalence_chart.R`: R script for a clustered bar chart.
- `smoking_cessation_map.R`: R script for an interactive map with bar overlays.
- Outputs: `smoking_prevalence_chart.png`, `smoking_cessation_map.html` (generated locally).

## Prerequisites
For beginners, here’s what you need:
- **Python**: Install from [python.org](https://www.python.org/downloads/). Use version 3.9+.
- **RStudio**: Download from [rstudio.com](https://rstudio.com/products/rstudio/download/). Install R first if prompted.
- **Text Editor**: Optional (e.g., Notepad, VS Code) to edit scripts.

## Step-by-Step Instructions

### 1. Set Up Your Environment
#### For Python (New Users)
1. **Install Python**:
   - Download and run the installer. Check "Add Python to PATH" during setup.
   - Open Command Prompt (Windows: `cmd`) and verify: `python --version` (e.g., Python 3.11.0).
2. **Install pandas**:
   - In Command Prompt: `pip install pandas`
   - If `pip` fails, try: `python -m ensurepip --upgrade` then `python -m pip install --upgrade pip`.

#### For RStudio (Fairly New Users)
1. **Install RStudio**:
   - After installing R, run the RStudio installer. Open RStudio to confirm it works.
2. **Install R Packages**:
   - In RStudio’s console (bottom left), run:
     ```R
     install.packages(c("ggplot2", "dplyr", "leaflet", "plotly", "htmltools", "htmlwidgets"))
     ```
   - Wait for each to install (takes a few minutes).

### 2. Generate the Data with Python
#### Script: `create_smoking_cessation_analysis_extended.py`
```python
import pandas as pd

# Simulated data for veteran smoking cessation
data = {
    "Age Range": ["50-54", "55-59", "60-64", "65-70"],
    "Smoking Prevalence (%)": [25.1, 22.8, 19.3, 15.7],
    "Pros of Today's Treatments": [
        "Nicotine patches and medications improve quitting success",
        "Behavioral therapy helps long-term cessation",
        "E-cigarettes may reduce cigarette consumption",
        "Medicare covers some smoking cessation programs"
    ],
    "Cons of Today's Treatments": [
        "Nicotine replacement can cause withdrawal symptoms",
        "Medications like Chantix may have side effects",
        "E-cigarettes still contain harmful chemicals",
        "Limited access to specialists in rural areas"
    ],
    "Why It Matters": [
        "Higher risk of lung disease, heart attacks",
        "Quitting reduces healthcare costs and improves quality of life",
        "Older smokers benefit significantly from cessation",
        "Health programs need better rural accessibility"
    ],
    "City": ["Carbondale", "Marion", "Herrin", "Murphysboro"],
    "Zip Code": ["62901", "62959", "62948", "62966"],
    "Latitude": [37.7273, 37.7306, 37.8031, 37.7645],
    "Longitude": [-89.2167, -88.9331, -89.0276, -89.3351]
}

# Create DataFrame and save to CSV
df = pd.DataFrame(data)
csv_filename = "C:/Users/Veteran/smoking_cessation_analysis_extended.csv"  # Change if not on Windows
df.to_csv(csv_filename, index=False)
print(f"CSV saved to: {csv_filename}")
```

#### Steps:
1. **Save the Script**:
   - Copy the code into a text editor, save as `create_smoking_cessation_analysis_extended.py` in `C:/Users/Veteran` (or your preferred folder).
2. **Run It**:
   - Open Command Prompt: `cd C:\Users\Veteran`
   - Type: `python create_smoking_cessation_analysis_extended.py`
   - Look for: `CSV saved to: C:/Users/Veteran/smoking_cessation_analysis_extended.csv`
3. **Check**: Open File Explorer to confirm the `.csv` is in `C:/Users/Veteran`.

### 3. Visualize with RStudio
#### Visualization 1: Clustered Bar Chart
**Script: `smoking_prevalence_chart.R`**
```R
library(ggplot2)
library(dplyr)

setwd("C:/Users/Veteran")
smoking_data <- read.csv("smoking_cessation_analysis_extended.csv")

p <- ggplot(smoking_data, aes(x = `Age.Range`, y = `Smoking.Prevalence....`, fill = `Age.Range`)) +
  geom_bar(stat = "identity", width = 0.7) +
  geom_text(aes(label = `Why.It.Matters`, y = `Smoking.Prevalence....` + 1), 
            size = 3, vjust = -0.5, hjust = 0, angle = 45) +
  labs(title = "Smoking Prevalence by Age Range (50-70)",
       subtitle = "With Key Health Impacts",
       x = "Age Range", y = "Smoking Prevalence (%)") +
  scale_fill_manual(values = c("50-54" = "#FF6F61", "55-59" = "#6B5B95", 
                               "60-64" = "#88B04B", "65-70" = "#F7CAC9")) +
  theme_minimal() +
  theme(legend.position = "none")

print(p)
ggsave("smoking_prevalence_chart.png", p, width = 10, height = 6, dpi = 300)
cat("Chart saved to:", getwd(), "/smoking_prevalence_chart.png\n")
```

#### Steps:
1. **Save the Script**:
   - In RStudio, click “File” > “New File” > “R Script”. Paste the code, save as `smoking_prevalence_chart.R` in `C:/Users/Veteran`.
2. **Run It**:
   - Click “Source” (top right) or press Ctrl+Shift+S to run the whole script.
   - See the chart in the “Plots” pane (bottom right).
3. **Output**: `smoking_prevalence_chart.png` in `C:/Users/Veteran`.

#### Visualization 2: Interactive Map with Bar Overlays
**Script: `smoking_cessation_map.R`**
```R
library(leaflet)
library(plotly)
library(dplyr)
library(htmltools)
library(htmlwidgets)

setwd("C:/Users/Veteran")
smoking_data <- read.csv("smoking_cessation_analysis_extended.csv")

map <- leaflet(smoking_data) %>%
  addTiles() %>%
  setView(lng = -89.2167, lat = 37.7273, zoom = 9) %>%
  addCircles(
    lng = ~Longitude, lat = ~Latitude,
    radius = ~`Smoking.Prevalence....` * 10000,
    color = "blue", fillOpacity = 0.5,
    popup = ~paste(
      "City:", City, "<br>",
      "Zip:", `Zip.Code`, "<br>",
      "Age Range:", `Age.Range`, "<br>",
      "Smoking Prevalence:", `Smoking.Prevalence....`, "%"
    )
  )

bar_charts <- lapply(1:nrow(smoking_data), function(i) {
  plot_ly(
    data = smoking_data[i, ],
    x = ~`Age.Range`, y = ~`Smoking.Prevalence....`,
    type = "bar",
    marker = list(color = "blue"),
    width = 150, height = 100
  ) %>%
    layout(
      title = paste(smoking_data$City[i], " (", smoking_data$Zip.Code[i], ")"),
      showlegend = FALSE,
      margin = list(l = 20, r = 20, t = 30, b = 20)
    )
})

map <- htmlwidgets::prependContent(
  map,
  tags$div(style = "position:absolute; top:10px; left:10px; z-index:1000;", bar_charts[[1]]),
  tags$div(style = "position:absolute; top:10px; right:10px; z-index:1000;", bar_charts[[2]]),
  tags$div(style = "position:absolute; bottom:10px; left:10px; z-index:1000;", bar_charts[[3]]),
  tags$div(style = "position:absolute; bottom:10px; right:10px; z-index:1000;", bar_charts[[4]])
)

print(map)
saveWidget(map, "smoking_cessation_map.html")
cat("Interactive map saved to:", getwd(), "/smoking_cessation_map.html\n")
```

#### Steps:
1. **Save the Script**:
   - New R Script in RStudio, paste the code, save as `smoking_cessation_map.R` in `C:/Users/Veteran`.
2. **Run It**:
   - Click “Source” or Ctrl+Shift+S.
   - Map appears in the “Viewer” pane (bottom right) or browser.
3. **Output**: `smoking_cessation_map.html` in `C:/Users/Veteran`. Open in a browser to interact.

### 4. Troubleshooting
- **Python Errors**:
  - `pip install pandas` if “module not found” appears.
  - Adjust `csv_filename` path (e.g., `/home/user/` on Linux/Mac).
- **RStudio Errors**:
  - If `.csv` not found, check `list.files("C:/Users/Veteran")`.
  - If packages fail, reinstall them in RStudio’s console.
- **Windows Path**: Use `/` or `\\` (e.g., `C:\\Users\\Veteran`).

### 5. Explore the Results
- **Bar Chart**: PNG shows prevalence with “Why It Matters” text.
- **Map**: HTML file maps cities with circles and bar overlays. Click circles for details.

## Next Steps
- Add to your GitHub: Clone this repo, run locally, and push outputs.
- Expand: More cities or health metrics? Let me know!

## Contact
Questions? Connect with me on LinkedIn or open an issue here!

<img width="959" alt="Screenshot 2025-03-20 211252" src="https://github.com/user-attachments/assets/95194124-5352-44d4-af64-97a1ad6c7467" />
<img width="957" alt="Screenshot 2025-03-20 211214" src="https://github.com/user-attachments/assets/e42b74ce-7456-4e02-b9f3-53aab9f1abde" />
```

---

### Steps to Create the Repository
1. **Create on GitHub**:
   - Go to GitHub, click “New Repository,” name it `Veteran-Smoking-Cessation-Visualizer`, initialize with a README.
   - Replace the default README with the content above, updating paths if needed.

2. **Add Files Locally**:
   - Save the Python script as `create_smoking_cessation_analysis_extended.py`.
   - Save R scripts as `smoking_prevalence_chart.R` and `smoking_cessation_map.R`.
   - Run both to generate outputs.
   - In `C:/Users/Veteran`:
     ```bash
     git init
     git add create_smoking_cessation_analysis_extended.py smoking_prevalence_chart.R smoking_cessation_map.R smoking_prevalence_chart.png smoking_cessation_map.html
     git commit -m "Initial commit with smoking cessation visualizer"
     git remote add origin https://github.com/yourusername/Veteran-Smoking-Cessation-Visualizer.git
     git push -u origin main
     ```

3. **Verify**: Check your GitHub repo online.

---

### Why This README Works
- **Beginner-Friendly**: Step-by-step with clear explanations and screenshots-like guidance.
- **Comprehensive**: Includes all code and troubleshooting.
- **Professional**: Showcases your skills for a portfolio.

Let me know if you’d like a different repo name or tweaks to the README! Ready to push this live? 🚀





