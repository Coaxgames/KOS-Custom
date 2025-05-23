.. _waypoint:

Waypoints
=========

.. contents::
    :local:
    :depth: 2

Waypoints are the location markers you can see on the map view showing you where contracts are targeted for.  With this structure, you can obtain coordinate data for the locations of these waypoints.

.. function:: WAYPOINT(name)

    :parameter name: (:struct:`String`) Name of the waypoint as it appears on the map or in the contract description
    :return: :struct:`Waypoint`

    This creates a new Waypoint from a name of a waypoint you read from the contract parameters.  Note that this only works on contracts you've accepted.  Waypoints for proposed contracts haven't accepted yet  do not actually work in kOS.

    SET spot TO WAYPOINT("herman's folly beta").

    The name match is case-insensitive.

.. function:: ALLWAYPOINTS()

    :return: :struct:`List` of :struct:`Waypoint`

    This creates a :struct:`List` of :struct:`Waypoint` structures for all accepted contracts.  Waypoints for proposed contracts you haven't accepted yet do not appear in the list.

.. structure:: Waypoint

    .. list-table:: **Members**
        :widths: 1 1
        :header-rows: 1

        * - Suffix
          - Type

        * - :attr:`NAME`
          - :struct:`String`
        * - :attr:`BODY`
          - `BodyTarget`
        * - :attr:`GEOPOSITION`
          - `GeoCoordinates`
        * - :attr:`POSITION`
          - `Vector`
        * - :attr:`ALTITUDE`
          - :struct:`Scalar`
        * - :attr:`AGL`
          - :struct:`Scalar`
        * - :attr:`NEARSURFACE`
          - :struct:`Boolean`
        * - :attr:`GROUNDED`
          - :struct:`Boolean`
        * - :attr:`INDEX`
          - :struct:`Scalar`
        * - :attr:`CLUSTERED`
          - :struct:`Boolean`
        * - :attr:`ISSELECTED`
          - :struct:`Boolean`


.. attribute:: Waypoint:NAME

    :type: :struct:`String`
    :access: Get only

    Name of waypoint as it appears on the map and contract

.. attribute:: Waypoint:BODY

    :type: `BodyTarget`
    :access: Get only

    Celestial body the waypoint is attached to


.. attribute:: Waypoint:GEOPOSITION

    :type: GeoCoordinates
    :access: Get only

    The LATLNG of this waypoint

.. attribute:: Waypoint:POSITION

    :type: Vector
    :access: Get only

    The Vector position of this waypoint in 3D space, in ship-raw coords.

.. attribute:: Waypoint:ALTITUDE

    :type: :struct:`Scalar`
    :access: Get only

    Altitude of waypoint **above "sea" level**.  Warning, this a point somewhere in the midst of the contract altitude range, not the edge of the altitude range.  It corresponds to where the marker tip hovers on the map, which is not actually at the very edge of the contract condition's range.  It represents a typical middling location inside the contract's altitude range.


.. attribute:: Waypoint:AGL

    :type: :struct:`Scalar`
    :access: Get only

    Altitude of waypoint **above ground**.  Warning, this a point somewhere in the midst of the contract altitude range, not the edge of the altitude range.  It corresponds to where the marker tip hovers on the map, which is not actually at the very edge of the contract condition's range.  It represents a typical middling location inside the contract's altitude range.


.. attribute:: Waypoint:NEARSURFACE

    :type: :struct:`Boolean`
    :access: Get only

    True if waypoint is a point near or on the body rather than high in orbit.


.. attribute:: Waypoint:GROUNDED

    :type: :struct:`Boolean`
    :access: Get only

    True if waypoint is actually glued to the ground.

.. attribute:: Waypoint:INDEX

    :type: :struct:`Scalar`
    :access: Get only

    The integer index of this waypoint amongst its cluster of sibling waypoints.  In other words, when you have a cluster of waypoints called "Somewhere Alpha", "Somewhere Beta", and "Somewhere Gamma", then the alpha site has index 0, the beta site has index 1 and the gamma site has index 2. When Waypoint:CLUSTERED is false, this value is zero but meaningless.

.. attribute:: Waypoint:CLUSTERED

    :type: :struct:`Boolean`
    :access: Get only

    True if this waypoint is part of a set of clustered waypoints with greek letter names appended (Alpha, Beta, Gamma, etc).  If true, there should be a one-to-one correspondence with the greek letter name and the :INDEX suffix. (0 = Alpha, 1 = Beta, 2 = Gamma, etc).

.. attribute:: Waypoint:ISSELECTED

    :type: :struct:`Boolean`
    :access: Get only

    True if navigation has been activated on this waypoint.
