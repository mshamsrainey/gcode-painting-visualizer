# Visualizing and Validating G-Code for Two-Dimensional Artistic Use (visualizer.py)

Simulating output of G-Code with semantic metadata used to render watercolor or (colored or black) pen artworks using human-like movements and technique.

Research poster [here](https://tinyurl.com/gcodeposter).

## Instructions for use

1. Open command line/terminal from the project directory (ex. cd ~/art-bot-drawing)
2. Run program using Python using the command: "python ./visualizer.py" along with the following command line arguments/switches

* -v: Verbose setting--Include this flag to print debug statements
* gcode_file_path: Path to G-Code file you would like visualized
* output_type: The algorithm can generate G-code to render the given image using three different artistic media techniques. To select which type of media output you want, set output_type to 0 for a pen outline, 1 for multiple colored pens, and 2 for watercolors.
* xDim and yDim: optional arguments (in mm). The defaults for these are the x and y dimensions of the original CNC machine that we used, and the dimensions for our string bot are 400mm by 600mm.
* resolution: conversion factor between millimeters declared in G-code and pixel resolution (recommended value between 50 and 100 for the CNC machine and 1-50 for the string bot)

Example use: python ./visualizer.py ./watercolor/gcode/mike.gcode 100 2
With these command line arguments, the visualizer will run using color and watercolor settings (wider pen width and translucent alpha value), with a resolution conversion factor of 100 at our default CNC dimensions. It will access the G-Code instructions contained in the file "mike.gcode" at the given relative path (absolute also works!) and create a digital rendering of what this G-Code would look like if painted by the CNC robot. This render will be stored as "mike_visualized.jpg" in the subdirectory folder for watercolor visualized_images and will be displayed immediately in your default photo viewing application.

## Background

In Fall 2021, I collaborated with a team of fellow CS/engineering students to develop hardware and software for "robots" (a modified CNC mill and an in-house string robot, both controlled using G-Code) capable of rendering a given image using human-like strokes. Using a standard G-Code similator, the G-Code to encode a painting or drawing, we found, was practically illegible--as G-Code is often used for three-dimensional surfaces, traditional simulators or visualizers showed movement both on and away from the canvas, whereas what we really wanted to see was the movement across that specific two-dimensional surface. Moreover, a traditional visualizer had no way to understand which color artistic instrument the machines were using, something very important to our final product!

In early stages, we solved for this by simply transmitting team members' programmatically-generated G-Code to the machine to draw or paint. This was sufficient for drawing simple shapes, and in fact essential for testing mechanical operations dependent on relative location in physical space (programming the machine to wash its paintbrush or load it with a new color). However, for rendering a drawing or painting based on a photograph, we quickly realized physical rendering could be incredibly time consuming. For some of our most complex pieces, physical rendering took up to two days!

To allow the team to iterate quickly and determine whether G-Code generation algorithms were working properly, I built this simple visualizer using NumPy and the Python Image Library. It takes in a file path for a pre-generated G-Code file with semantic metadata encoding color changes, brush cleaning, etc. as comments, parses it to render pen or brush strokes and save the resultant file for holistic comparison against the source image. Running in a 0-5 minutes, this visualizer gave us nearly real-time feedback.

## Disclaimers, Credits, etc

The code presented here is presented as-is, and represents a small part of a larger project through Duke University's ECE Department. While this code and my work on it are technically independent of other project sections, it was deeply intertwined with our workflow, especially in the later stages of the project. To that end, the G-Code presented and rendered here is also the work of my teammates. You can find our team's working repository [here](https://github.com/evankenyon/art-bot-drawing).
