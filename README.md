# Blazor in .NET 8: Sample 5

Let's delve into a Blazor example that showcases how to work with JavaScript interoperability, a powerful technique for integrating existing JavaScript libraries or custom functions into your Blazor applications.

**Example: Interactive Chart**

**Features Demonstrated**:

**JavaScript Interop**: Calling JavaScript functions from C# and vice versa

**External Libraries**: Leveraging a JavaScript charting library (we'll use Chart.js)

**Prerequisites**

Basic understanding of Blazor and JavaScript

Familiarity with a Charting library would be helpful, but not strictly required

**Setup**

**Create Project**:  Start with a new Blazor Server project (or reuse an existing one). You can name it "ChartingApp"

**Install Chart.js**:

**Option 1**: NPM: If you're familiar with npm, install Chart.js:

```
npm install chart.js
```

**Option 2**: Manual Download: Download the latest Chart.js distribution from https://www.chartjs.org/ and place the chart.min.js file into your project's wwwroot folder

**Import Script**: In your index.html (or _Host.cshtml if using Razor Pages), include the Chart.js script within the <head> section:

```html
<script src="chart.min.js"></script> 
```

**Components**

**ChartComponent.razor: (Inside the Pages folder)**

```cshtml
@page "/chart"
@inject IJSRuntime JSRuntime 

<h1>Interactive Chart</h1>

<canvas id="myChart" width="400" height="200"></canvas>

@code {
    protected override async Task OnAfterRenderAsync(bool firstRender)
    {
        if (firstRender)
        {
            await JSRuntime.InvokeVoidAsync("initializeChart", "myChart", sampleData);
        }
    }

    // Sample data for the chart
    private object[] sampleData = new object[]  { 12, 19, 3, 5, 2, 3 }; 
}
```

**wwwroot/index.html (or _Host.cshtml)**:

Add the following JavaScript function inside your <script> section:

```javaScript
window.initializeChart = (canvasId, data) => {
    let ctx = document.getElementById(canvasId).getContext('2d');
    new Chart(ctx, {
        type: 'bar',
        data: {
            labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
            datasets: [{
                label: 'Sample Data',
                data: data,
                // ... more chart customization options
            }]
        },
    });
};
```

Let me know if you'd like to explore more advanced scenarios such as updating the chart dynamically, integrating other JavaScript libraries, or creating custom JavaScript functions for your Blazor components!


