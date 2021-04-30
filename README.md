# de1-flow-calibration-estimation

Use python 3.8+ with following packages:
- matplotlib
- scipy
- numpy
- esprima
- requests

``` 
(venv) de1-flow-calibration-estimation> python -m flowcorrection [-h] [--visualizer [VISUALIZER_URL] | --file [FILE]]
```
- `--visualizer [URL]`: specify shot URL on the visualizer site (or will be asked) 
- `--file [PATH]`: specify a shot file (or will be asked)
- or without any option: you'll be asked to pick a shot file

Sample shots are available in the example directory.

## Simple (or maybe too verbose) Guide

Pick a shot that meets following requirements:
- It has the weight data measured from a BT scale
- It came from an actual coffee extraction
  (<span style="font-weight:bold">not from like a calibration basket</span>),
- And it was stable without a massive channeling or so
- It has a pressure declining stage towards the end
  - "Londinium style" profile is usually a good choice (as shown in the screenshot below)
- Or, at least, can be considered a simple and neat "fully saturate, then squeeze" style shot
  - no pause in the middle
  - reasonably good pressure during the extraction  

![flowcorrection](figure.png)

1. Move optimization window slider (horizontal one) to desired position
    - Typical GOOD region to include: where you think the extraction is stable
      - 3 bars < pressure < 9 bars
      - 1 ml/s < flow < 4 ml/s
    - Typical BAD region to include:
      - coffee just began dropping
      - flow or weight value is spiking
      - pressure is too low (like under 2 bars)
      - flow is too low (like under 1 ml/s)

1. Suggested correction value(<span style="color:pink;font-weight:bold">horizontal pink line</span>)
   also changes as you adjust the optimization window
   
1. Then adjust correction slider (vertical one) to see if <span style="color:blue;font-weight:bold">corrected flow</span>
   well-fits <span style="color:brown;font-weight:bold">measured weight</span> within the window
   - <span style="color:magenta;font-weight:bold">Correction line</span>
    also moves as you adjust the correction value
   - So, first, try to move <span style="color:magenta;font-weight:bold">correction line</span>
     closer to the <span style="color:pink;font-weight:bold">suggestion line</span>
   ![move_correction_line](figure_correction.png)   

1. Use the correction value just found as a starting point finding flow calibration value in the DE1 app.
