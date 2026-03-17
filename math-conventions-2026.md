---
layout: default
title: Mathematical Conventions Survey 2026
---

<style>
  .conventions-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem 1rem;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
    color: #333;
  }
  
  .conventions-header {
    text-align: center;
    margin-bottom: 3rem;
  }
  
  .conventions-header h1 {
    font-size: 2.5rem;
    font-weight: 700;
    margin-bottom: 1rem;
    color: #1a1a1a;
  }
  
  .conventions-header p {
    font-size: 1.1rem;
    color: #666;
    max-width: 800px;
    margin: 0 auto;
    line-height: 1.6;
  }
  
  .charts-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
    gap: 2rem;
  }
  
  .chart-card {
    background: #fff;
    border-radius: 12px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05), 0 1px 3px rgba(0, 0, 0, 0.1);
    padding: 1.5rem;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
    display: flex;
    flex-direction: column;
  }
  
  .chart-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 15px rgba(0, 0, 0, 0.1), 0 4px 6px rgba(0, 0, 0, 0.05);
  }
  
  .chart-title {
    font-size: 1.1rem;
    font-weight: 600;
    margin-bottom: 1.5rem;
    color: #2d3748;
    line-height: 1.4;
    text-align: center;
    flex-grow: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 3em;
  }
  
  .chart-wrapper {
    position: relative;
    height: 250px;
    width: 100%;
    margin-top: auto;
  }
  
  .loading {
    text-align: center;
    padding: 4rem;
    font-size: 1.2rem;
    color: #666;
  }
  
  .spinner {
    display: inline-block;
    width: 40px;
    height: 40px;
    border: 4px solid rgba(0, 0, 0, 0.1);
    border-radius: 50%;
    border-top-color: #4299e1;
    animation: spin 1s ease-in-out infinite;
    margin-bottom: 1rem;
  }
  
  @keyframes spin {
    to { transform: rotate(360deg); }
  }
  
  .error-message {
    background: #fed7d7;
    color: #c53030;
    padding: 1rem;
    border-radius: 8px;
    text-align: center;
    margin: 2rem 0;
  }
  
  .custom-legend {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 1rem;
    padding: 1rem 0;
    font-size: 0.95rem;
    color: #4A5568;
    margin-top: 10px;
  }
  
  .legend-item {
    display: flex;
    align-items: center;
    gap: 0.4rem;
  }
  
  .legend-color {
    width: 14px;
    height: 14px;
    border-radius: 50%;
    display: inline-block;
  }
</style>

<div class="conventions-container">
  <div class="conventions-header">
    <h1>Mathematical Conventions Survey 2026</h1>
    <p>Results from the 2026 Faculty-Student Mixer. We asked 30 questions about mathematical conventions to find out where our department stands on the most pressing issues in mathematics.</p>
  </div>
  
  <div id="loading-state" class="loading">
    <div class="spinner"></div>
    <div>Loading survey data...</div>
  </div>
  
  <div id="error-state" class="error-message" style="display: none;"></div>
  
  <div id="charts-container" class="charts-grid" style="display: none;">
    <!-- Charts will be generated here -->
  </div>
</div>

<!-- Load MathJax for rendering LaTeX -->
<script>
  window.MathJax = {
    tex: {
      inlineMath: [['$', '$'], ['\\(', '\\)']]
    },
    svg: {
      fontCache: 'global'
    },
    startup: {
      typeset: false // We will manually typeset after rendering charts
    }
  };
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js"></script>

<!-- Load PapaParse for CSV parsing -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.4.1/papaparse.min.js"></script>
<!-- Load Chart.js for visualizations -->
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<script>
  // Questions mapped to their respective columns in the CSV using exact LaTeX from Conventions.tex
  const questions = [
    { id: "Q1", text: "1. Is $0\\in \\mathbb{N}$?" },
    { id: "Q2", text: "2. What is $0^0$?" },
    { id: "Q3", text: "3. What is $\\sqrt{-1}$?" },
    { id: "Q4", text: "4. What is the sum of two integers?" },
    { id: "Q5", text: "5. What is the quotient of two integers?" },
    { id: "Q6", text: "6. Is the empty graph connected?" },
    { id: "Q7", text: "7. Is $f(x)=3$ increasing?" },
    { id: "Q8", text: "8. Fill in the blank: $2\\mathbb{Z}=\\{n\\in \\mathbb{Z}\\quad \\underline{~~~~} \\quad n \\text{ is even}\\}$." },
    { id: "Q9", text: "9. What is the eigenvalue problem for the Laplacian?" },
    { id: "Q10", text: "10. What is the Fourier Transform of $f$?" },
    { id: "Q11", text: "11. Numbers..." },
    { id: "Q12", text: "12. What is $\\mathbb{Z}_p$?" },
    { id: "Q13", text: "13. Do you accept the axiom of choice?" },
    { id: "Q14", text: "14. Are rings commutative?" },
    { id: "Q15", text: "15. Are rings unital?" },
    { id: "Q16", text: "16. What is the group of symmetries of a regular $n$-gon?" },
    { id: "Q17", text: "17. What is the symbol for the Lebesgue measure?" },
    { id: "Q18", text: "18. Let $a$ and $x$ be elements of a group. What is the conjugation of $x$ via $a$?" },
    { id: "Q19", text: "19. What is the base of $\\log$?" },
    { id: "Q20", text: "20. For $x\\in \\mathbb{R}^n$, what is the norm of $x$?" },
    { id: "Q21", text: "21. What is the range of $f:X\\to Y$?" },
    { id: "Q22", text: "22. What is $\\log^2(x)$?" },
    { id: "Q23", text: "23. What is the set of limit points of $\\{1\\}$?" },
    { id: "Q24", text: "24. Is $f(x)=\\frac{1}{x}$ continuous?" },
    { id: "Q25", text: "25. When integrating, the symbol for the differential should be ..." },
    { id: "Q26", text: "26. A signed measure..." },
    { id: "Q27", text: "27. What is the usual variable name for the Yoneda embedding?" },
    { id: "Q28", text: "28. What is the pronunciation of \"\\LaTeX\"?" },
    { id: "Q29", text: "29. Is $f(x)=3x+1$ linear?" },
    { id: "Q30", text: "30. What is the value of $6\\div2(1+2)$?" }
  ];

  // Beautiful, vibrant color palette
  const colorPalette = [
    '#4299E1', // Blue
    '#F56565', // Red
    '#48BB78', // Green
    '#ED8936', // Orange
    '#9F7AEA', // Purple
    '#38B2AC', // Teal
    '#ECC94B', // Yellow
    '#ED64A6', // Pink
    '#A0AEC0', // Gray
    '#667EEA', // Indigo
  ];

  document.addEventListener("DOMContentLoaded", function() {
    // Fetch the CSV file
    fetch('{{ site.baseurl }}/assets/faculty-student-mixer/2026/answers.csv')
      .then(response => {
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        return response.text();
      })
      .then(csvText => {
        // Parse the CSV
        Papa.parse(csvText, {
          header: true,
          skipEmptyLines: true,
          complete: function(results) {
            const data = results.data;
            renderCharts(data);
          },
          error: function(error) {
            showError(`Error parsing CSV: ${error.message}`);
          }
        });
      })
      .catch(error => {
        showError(`Failed to load survey data: ${error.message}. Make sure the file exists at /assets/faculty-student-mixer/2026/answers.csv`);
      });
  });

  function showError(message) {
    document.getElementById('loading-state').style.display = 'none';
    const errorEl = document.getElementById('error-state');
    errorEl.textContent = message;
    errorEl.style.display = 'block';
  }

  function renderCharts(data) {
    // Hide loading, show charts container
    document.getElementById('loading-state').style.display = 'none';
    const container = document.getElementById('charts-container');
    container.style.display = 'grid';

    // Set common Chart.js defaults for a cleaner look
    Chart.defaults.font.family = '-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif';
    Chart.defaults.color = '#4A5568';
    
    // Create a chart for each question
    questions.forEach((q, index) => {
      // Create DOM elements for the chart
      const card = document.createElement('div');
      card.className = 'chart-card';
      
      const title = document.createElement('h3');
      title.className = 'chart-title';
      title.innerHTML = q.text; // InnerHTML to parse mathematical symbols
      
      const wrapper = document.createElement('div');
      wrapper.className = 'chart-wrapper';
      
      const canvas = document.createElement('canvas');
      canvas.id = `chart-${q.id}`;
      
      const legendContainer = document.createElement('div');
      legendContainer.className = 'custom-legend';
      legendContainer.id = `legend-${q.id}`;
      
      wrapper.appendChild(canvas);
      card.appendChild(title);
      card.appendChild(wrapper);
      card.appendChild(legendContainer); // Add legend below wrapper
      container.appendChild(card);
      
      // Process data for this question
      const answerCounts = {};
      
      data.forEach(row => {
        let answer = row[q.id];
        
        // Skip empty answers
        if (!answer || answer.trim() === '') return;
        
        answer = answer.trim();
        
        // Let's add $ around exact math strings to give MathJax a better chance 
        // if they aren't already formatted with $ (though some are like \hat{f})
        // For simplicity we just render them directly, users will enter math
        
        answerCounts[answer] = (answerCounts[answer] || 0) + 1;
      });
      
      // Prepare chart data
      const labels = Object.keys(answerCounts);
      
      // If no valid answers for this question, skip chart creation
      if (labels.length === 0) {
        wrapper.innerHTML = '<div style="display:flex; height:100%; align-items:center; justify-content:center; color:#a0aec0; font-style:italic;">No responses</div>';
        return;
      }
      
      const counts = Object.values(answerCounts);
      
      // Select colors based on the number of answers to ensure variety
      const bgColors = labels.map((_, i) => colorPalette[i % colorPalette.length]);
      // Slightly transparent background colors with opaque borders
      const bgColorsAlpha = bgColors.map(color => {
        // Simple hex to rgba conversion since we know our palette is hex
        const r = parseInt(color.slice(1, 3), 16);
        const g = parseInt(color.slice(3, 5), 16);
        const b = parseInt(color.slice(5, 7), 16);
        return `rgba(${r}, ${g}, ${b}, 0.8)`;
      });
      
      // Build custom HTML legend
      labels.forEach((label, i) => {
        const item = document.createElement('div');
        item.className = 'legend-item';
        
        const colorBox = document.createElement('span');
        colorBox.className = 'legend-color';
        colorBox.style.backgroundColor = bgColorsAlpha[i];
        colorBox.style.border = `1px solid ${bgColors[i]}`;
        
        const textSpan = document.createElement('span');
        textSpan.className = 'legend-text';
        // Wrap with inline math if it contains backslashes and doesn't have $
        let formattedLabel = label;
        if (label.includes('\\') && !label.includes('$')) {
            formattedLabel = `$${label}$`;
        } else if (label === "m/n" || label === "n/m" || label === "a/b" || label === "m+n" || label === "n+m") {
            formattedLabel = `$${label}$`;
        }
        textSpan.innerHTML = formattedLabel;
        
        item.appendChild(colorBox);
        item.appendChild(textSpan);
        legendContainer.appendChild(item);
      });
      
      // Render the chart
      new Chart(canvas, {
        type: 'doughnut',
        data: {
          labels: labels,
          datasets: [{
            data: counts,
            backgroundColor: bgColorsAlpha,
            borderColor: '#ffffff',
            borderWidth: 2,
            hoverOffset: 6
          }]
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          plugins: {
            legend: {
              display: false // Disable standard legend
            },
            tooltip: {
              backgroundColor: 'rgba(26, 32, 44, 0.9)',
              titleFont: { size: 13 },
              bodyFont: { size: 14, weight: 'bold' },
              padding: 12,
              cornerRadius: 8,
              callbacks: {
                label: function(context) {
                  const label = context.label || '';
                  const value = context.raw;
                  const total = context.chart._metasets[context.datasetIndex].total;
                  const percentage = Math.round((value / total) * 100);
                  return ` ${label}: ${value} (${percentage}%)`;
                }
              }
            }
          },
          cutout: '60%' // Make it a nice doughnut shape
        }
      });
    });
    
    // Typeset MathJax now that the DOM is populated
    if (window.MathJax && window.MathJax.typesetPromise) {
      window.MathJax.typesetPromise([container]).catch(function (err) {
        console.error('MathJax formatting failed: ' + err.message);
      });
    }
  }
</script>
