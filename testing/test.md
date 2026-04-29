---
theme: consult
---

# Progress

<style>
  :root {
    --color-enova: #324947;
    --color-crayon: #FF6A4C;
  }
  .progress-bar-outer {
    position: relative;
    width: 100%;
    height: 20px;
    margin-bottom: 4px;
  }
  .progress-bar {
    width: 100%;
    background: #eee;
    border-radius: 4px;
    height: 100%;
    display: flex;
    overflow: hidden;
    position: absolute;
    left: 0;
    top: 0;
  }
  .progress-bar-overflow {
    position: absolute;
    left: 0;
    top: 0;
    height: 100%;
    border: 2px solid #000;
    border-radius: 4px;
    box-sizing: border-box;
    pointer-events: none;
  }
  .progress-bar-dotted {
    position: absolute;
    top: 0;
    bottom: 0;
    width: 2px;
    border-left: 2px dotted #000;
    background: none;
    opacity: 1;
    pointer-events: none;
  }
</style>
<div style="margin-bottom: 8px;">Oktober: 165 timer av 172.5 (95.7%)</div>
<div class="progress-bar-outer" style="width: 100%; max-width: 100%;">
  <div class="progress-bar" style="width: ((166/171)*10)%;">
    <div style="width: 90.7%; background: var(--color-enova);"></div>
    <div style="width: 9.26%; background: var(--color-crayon);"></div>
  </div>
  <div class="progress-bar-overflow" style="width: 100%;"></div>
  <div class="progress-bar-dotted" style="left: 85%;"></div>
</div>
<script>
console.log("hello")
</script>

---

# Chart

```chart
    type: bar
    labels: [Monday,Tuesday,Wednesday,Thursday,Friday, Saturday, Sunday, "next Week", "next Month"]
    series:
        - title: Title 1
        data: [1,2,3,4,5,6,7,8,9]
        - title: Title 2
        data: [5,4,3,2,1,0,-1,-2,-3]
```

---
<canvas data-chart="bar" >
Month, October
Enova, 158.5
Crayon, 15.5
Overflow, 13
<!--
{
  "data": {
    "datasets": [
      { "backgroundColor": "#324947" },
      { "backgroundColor": "#FF6A4C" },
      { "backgroundColor": "#888", "label": "Overflow" }
    ]
  },
  "options": {
    "indexAxis": "y",
    "scales": {
      "x": {
        "stacked": true,
        "position": "top",
        "title": { "display": true, "text": "Hours" },
        "max": 200,
        "grid": { "color": "#ccc" },
        "ticks": { "stepSize": 172.5 }
      },
      "xPercent": {
        "type": "linear",
        "position": "bottom",
        "min": 0,
        "max": 120,
        "title": { "display": true, "text": "Percent" },
        "grid": { "color": "#555" },
        "ticks": {
          "stepSize": 85,
          "color": "#ccc"
        }
      },
      "y": {
        "stacked": true
      }
    }
  }
}
-->
</canvas>
