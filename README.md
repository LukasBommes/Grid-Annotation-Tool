# Grid Annotation Tool

A tool for annotating grid structures in images for computer vision research and applications. For some applications you may want to annotate a grid structure to train, for example, an instance segmentation model, such as Mask R-CNN.

Different from existing annotation tools you do not have to draw a bounding box for each cell in your grid. Instead, you annotate the intersection lines, which is faster and yields cleaner co-linear edges. To account for lens distortion you can annotate both lines and curves.

We initially developed this tool for annotating instance segmentation masks of photovoltaics modules, but it may be useful for other applications.


### Installation

This project requires Python 3, [Flask](https://pypi.org/project/Flask/) and [Flask-WTF](https://pypi.org/project/Flask-WTF/).


### Quickstart

1. Open a terminal in the project root and run `python annotation_tool.py`
2. Navigate to 127.0.0.1:5000 in your web browser

You should now see the annotation app and a list of example images in the left sidebar. You can click on one of the images and begin annotation.


### Annotating your own images

1. Rename your images with random UUID4 (e.g. with Python's UUID library)
2. Place your images in `static/uploads`
3. Start the annotation tool as explained above


### Annotating a Grid

1. Select an image in the left sidebar by clicking on one of the image IDs
2. Draw auxiliary lines / auxiliary curves by clicking on "Draw Auxiliary Line" / "Draw Auxiliary Curve" and placing two / three points by clicking into the image. These lines should outline the grid lines between individual grid cells.
3. Click on "Get Intersections" to compute the intersection points between auxiliary lines and curves.
4. You can optionally add intersection points manually by clicking "Add corners" and placing them in the image by clicking.
5. Click on "Create Grid Cell" to indicate which corners belong to a grid cell. When hovering over the image four dashed lines will connect your cursor to four corner points. Move the cursor roughly in the center of the grid cell and click. A new grid cell is being placed.
6. If automatic selection of corner points is not possible, click "Create Grid Cell (manual)" and select the four corners of a grid cell by clicking.
7. If you want to handle truncated (i.e. partially visible) grid cells differently in your application, you can click the "Toggle Cell Visibility" button. Now, you can click on grid cells and mark them as truncated. A truncated grid cell will be rendered in yellow.

To erase items, such as corners or auxiliary lines, click the "Erase" button and click the item you want to delete in the image. When you erase a corner all associated grid cells will be removed.

You can drag auxiliary lines or corners in the image by clicking an dragging.


### Annotation File Format

To save the annotation simply go to the next image by selecting it in the left sidebar. The annotation is saved in a separate JSON file for each image under `static/annotations`. The file name corresponds to the image UUID. Another json file is placed under `static/save`, which is for internal use only.

The annotation file format is as follows, i.e. each image has a list of grid cells, each with four corner points, one center point, its own UUID and a boolean flag indicating whether the grid cell is truncated.
```
{
  "image": "0a002eb1-8d2c-4d23-8a25-65a34d1f2673.jpg",
  "grid_cells": [
    {
      "corners": [
        {"x": 181.98136043148975, "y": 180.87500292991302},
        {"x": 80.99062551749896, "y": 176.94569670353974},
        {"x": 78.42819076221744, "y": 294.24826550087346},
        {"x": 183.0432587489509, "y": 294.49812289825013}
      ],
      "center": {"x": 131.1108588650393, "y": 236.64177200814407},
      "id": "0d9307ac-0a57-48e9-897f-8d782e844509",
      "truncated": true
    },
    ...
  ]
}
```

### Known Bugs

The grid annotation tool relies on the [2D.js](http://www.kevlindev.com/geometry/2D/intersections/index.htm) library for calculating intersection points between auxiliary lines. It has a known bug, which causes it to miss some intersections between pairs of curves. In this case, please add the missed intersections manually by first clicking "Add Corners" and then clicking on the image.

### About

This software is written by **Lukas Bommes, M.Sc.** - [Helmholtz Institute Erlangen-Nürnberg for Renewable Energy](https://www.hi-ern.de/hi-ern/EN/home.html)


#### License

This project is licensed under the MIT license - see the [LICENSE](LICENSE) file for details.
