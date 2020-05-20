Coordinate systems
==================
In the file coordinate_systems.py are contained several classes to manipulate scenes containing coordinate systems.
This is useful for example to draw a function on a given range and scale.

.. raw:: html

    <video width="560" height="315" controls>
        <source src="_static/coordinate_systems/ExampleAxes.mp4" type="video/mp4">
    </video>

.. code-block:: python

        class CustomAxes(Axes):
            CONFIG = {
                "axis_config": {"unit_size": 0.5},
                "x_min": -1,
                "x_max": 4,
                "y_min": -1,
                "y_max": 10,
                "center_point": 2 * DOWN + 1.5 * LEFT,
            }


        class ExampleAxes(Scene):
            def construct(self):
                axes = CustomAxes()
                self.add(axes)
                graph = axes.get_graph(lambda x: x ** 2, x_min=0, x_max=3)
                self.play(ShowCreation(graph))
                self.wait()

The main purposes of such functions is to change the frame of reference and give some axes as indications.
The class ``CoordinateSystem`` is an abstract class with methods allowing the map between coordinates and points,
manipulation of axes and graph representation.

Axes
----
This class can be directly used to represent a 2D coordinate system.
It is also the super class for *ThreeDAxes* and *NumberPlanes*.
One can illustrate the features of CoordinateSystem with this class.

``coords_to_point(*coords)``:

Changes the coordinates given to point coordinates, numpy array.

``c2p(*coords)``:

Alias for coords_to_point.

.. raw:: html

    <video width="560" height="315" controls>
        <source src="_static/coordinate_systems/CoordsToPoint.mp4" type="video/mp4">
    </video>

.. code-block:: python

        class CoordsToPoint(Scene):
            def construct(self):
                axes = Axes()
                self.add(axes)
                dot = Dot(axes.c2p(1, 2))
                self.add(dot)
                self.wait()

``point_to_coords(point)``:

Changes the point to a tuple coordinates.

``p2c(*coords)``:

Alias for point_to_coords

.. raw:: html

    <video width="560" height="315" controls>
        <source src="_static/coordinate_systems/PointToCoords.mp4" type="video/mp4">
    </video>

.. code-block:: python

        class PointToCoords(Scene):
            def construct(self):
                axes = Axes()
                self.add(axes)
                coord = UP + 2 * LEFT
                dot = Dot(coord)
                self.add(dot)
                anno = TexMobject("{}".format(axes.p2c(coord)))
                anno.shift(UP + coord)
                self.add(anno)
                self.wait()
