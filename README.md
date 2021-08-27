This app can be used to manually annotate segmentation maps for photovoltaic modules.


### Quickstart

1) Rename your JPEG images with random UUID4 that can be generated for example with pythons UUID library
1) Insert your images into the directory `static/uploads`
2) Launch the tool from the root directory with the command `python flask_server.py`
3) In your webbrowser navigate to 127.0.0.1:5000

You should now see the annotation app.


### How to annotate PV modules

1) Select an image in the left sidebar by clicking on one of the image IDs
2) Draw auxiliary lines / auxiliary curves by clicking on "Draw Auxiliary Line" / "Draw Auxiliary Curve" and placing two / three points by clicking into the image. these lines should outline the grid lines between individual PV modules.
3) Click on "Get Intersections" to compute the intersection points between auxiliary lines and curves. When the auxiliary lines were placed correctly the intersections should approximately lie on the corners of the PV modules.
4) You can optionally annotate corners of PV modules manually by clicking "Add corners" and placing them in the image by clicking.
5) Click on "Create Modules" to indicate which corners belong to the same PV module. When hovering over the image four dashed lines will connect your cursor to four corner points. Move the cursor roughly in the center of a module and click. A new PV module is being placed.
6) In some cases the automatic selection of four corner points might not work. In these cases click "Create Modules (manual)" and select the four corners of a PV module by clicking. A PC module will be created.
7) You can add optional information to each module by clicking "Edit Module Details", clicking on a PV module and checking/unchecking the options in the left sidebar (e.g. "Module partially visible", "Hot cell(s)", etc.). Repeat this for every PV module you want to annotate.

To erase items, such as corners or auxiliary lines, choose the "Erase" tool and click the item in the image. When you erase a corner all associated PV modules will be removed.

You can drag auxiliary lines or corners in the image by clicking an dragging.


### Saving an annotation

To save the annotation simply go to the next image by slecting it in the left sidebar. The annotation is being saved automatically in the directory `static/annotations`. For each image a json file named with the same UUID4 as the corresponding image can be found. Another json file is placed under `static/save`. This file is for internal use and contains additional information which is not necessary for downstream tasks.