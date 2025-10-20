# Lozenge Donut Chart v2

An Atlassian Forge app that creates interactive donut chart visualizations from Confluence status lozenges (status badges). This Confluence macro scans the current page for status lozenges, counts them by label and color, and displays the results in a professional donut chart visualization.

## Overview

This macro is designed to help track blueprint standard adherence by visualizing the distribution of status lozenges across a Confluence page. It automatically:

- Scans the current Confluence page for all status lozenges (status macros)
- Counts lozenges by their label and color (e.g., "Standard (Green)", "Semi-Standard (Orange)", "Bespoke (Blue)")
- Displays the data in an interactive donut chart with proper color assignments
- Shows total count and meaningful subtitle text

## Features

- **Automatic Detection**: No manual configuration needed - just add the macro to any page
- **Smart Color Mapping**: Intelligently assigns chart colors based on lozenge types (Standard=Green, Semi-Standard=Orange, Bespoke=Blue)
- **Title Case Formatting**: Automatically converts lozenge labels to Title Case for consistent display
- **Real-time Updates**: Fetches current page content on each load to ensure accurate counts
- **User-Friendly Display**: Shows meaningful error messages and loading states

## Use Case

This macro is particularly useful for:
- **Blueprint Documentation**: Track compliance levels across documentation pages
- **Standard Adherence Tracking**: Visualize how well solutions follow organizational standards
- **Quality Metrics**: Quick visual summary of documentation quality indicators
- **Progress Tracking**: Monitor standardization efforts across multiple pages

## Technical Details

### Built With
- **Atlassian Forge** - Custom UI with React components
- **@forge/react** - Forge React UI Kit (DonutChart component)
- **@forge/api** - Confluence REST API integration
- **Node.js 22.x** - Runtime environment

### How It Works

1. **Backend Resolver** (`src/resolvers/index.js`):
   - Retrieves the current page ID from the Forge context
   - Fetches page content using Confluence API v2
   - Parses the storage format XML to find all status macros
   - Extracts title and color parameters from each lozenge
   - Returns aggregated counts to the frontend

2. **Frontend Component** (`src/frontend/index.jsx`):
   - Invokes the backend resolver to get lozenge data
   - Transforms data for the DonutChart component
   - Applies custom color ordering for standard visualization
   - Renders the chart with proper title and subtitle

### Lozenge Detection

The app uses regex pattern matching to find Confluence status macros in the page's storage format:

```xml
<ac:structured-macro ac:name="status">
  <ac:parameter ac:name="title">Standard</ac:parameter>
  <ac:parameter ac:name="colour">Green</ac:parameter>
</ac:structured-macro>
```

Supported colors: Grey, Red, Yellow, Green, Blue

## Requirements

See [Set up Forge](https://developer.atlassian.com/platform/forge/set-up-forge/) for instructions to get set up.

- Forge CLI installed and configured
- Node.js 18.x or later
- Access to a Confluence Cloud site for installation

## Installation & Deployment

### Quick Start

1. **Build and deploy your app:**
   ```bash
   forge deploy
   ```

2. **Install the app on your Confluence site:**
   ```bash
   forge install
   ```

3. **Add the macro to any Confluence page:**
   - Edit a page
   - Type `/` and search for "Lozenge Donut Chart"
   - Insert the macro
   - The chart will automatically display based on page content

### Development

- **Local development** with hot-reloading:
  ```bash
  forge tunnel
  ```

- **Modify the frontend** by editing `src/frontend/index.jsx`
- **Modify the backend** by editing `src/resolvers/index.js`

### Notes
- Use `forge deploy` when you want to persist code changes
- Use `forge install` when you want to install the app on a new site
- Once installed, the site picks up new deployments automatically (no reinstall needed)

## Permissions

The app requires the following Confluence permissions:
- `read:page:confluence` - To fetch page content and count lozenges

## Architecture

```
lozenge-donut-chart-v2-claude-code/
├── src/
│   ├── frontend/
│   │   └── index.jsx          # React UI component with DonutChart
│   ├── resolvers/
│   │   └── index.js            # Backend resolver for API calls
│   └── index.js                # Main entry point
├── static/                     # Static HTML examples/demos
├── manifest.yml                # Forge app configuration
└── package.json                # Dependencies
```

## Configuration

The macro works out-of-the-box with no configuration needed. However, you can customize:

- **Chart Title**: Currently set to "How compliant is this Blueprint with SeatGeek's standards?"
- **Color Order**: Defined in `colorPriorityOrder` array in `index.jsx`
- **Chart Height**: Currently 400px (adjustable via `height` prop)

## Example Output

When inserted on a page with lozenges, the macro displays:

- **Donut Chart** showing percentage breakdown
- **Legend** with color-coded labels and counts
- **Title** describing what the chart represents
- **Subtitle** showing total number of items counted

Example data visualization:
- Standard (Green): 45
- Semi-Standard (Orange): 30
- Bespoke (Blue): 25

## Troubleshooting

- **"No labeled solutions found"**: The page has no status lozenges or they're not in the expected format
- **"Could not retrieve page ID"**: Macro context is missing - try re-inserting the macro
- **"Failed to fetch page"**: API request failed - check app permissions and Confluence site access

## Version History

**v2 (Claude Code Edition)**
- Complete rewrite using Forge Custom UI
- Added React-based frontend with DonutChart component
- Improved lozenge parsing with regex
- Smart color assignment
- Title case formatting

## Documentation

- [Forge Documentation](https://developer.atlassian.com/platform/forge/)
- [Custom UI Resolver Reference](https://developer.atlassian.com/platform/forge/runtime-reference/custom-ui-resolver/)
- [Forge React Components](https://developer.atlassian.com/platform/forge/ui-components/)

## License

Part of the work-tools-portfolio showcase.

---

Built with [Claude Code](https://claude.com/claude-code)
