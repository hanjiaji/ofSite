#class ofMesh


<!--
_visible: True_
_advanced: False_
_istemplated: False_
_extends: _
-->

##InlineDescription

Represents a set of vertices in 3D spaces with normals, colors,
and texture coordinates at those points.

Each of these different properties is stored in a vector.
Vertices are passed to your graphics card and your graphics card fill in
the spaces in between them in a processing usually called the rendering
pipeline. The rendering pipeline goes more or less like this:

1. Say how you're going to connect all the points.
2. Make some points.
3. Say that you're done making points.

You may be thinking: I'll just make eight vertices and voila: a cube.
Not so quick. There's a hitch and that hitch is that the OpenGL renderer
has different ways of connecting the vertices that you pass to it and none
are as efficient as to only need eight vertices to create a cube.

You've probably seen a version of the following image somewhere before.
![PRIMATIVES](3d/primitives_new-640x269.gif)
Generally you have to create your points to fit the drawing mode that
you've selected because of whats called winding.
A vertex gets connected to another vertex in the order that the mode does
its winding and this means that you might need multiple vertices in a given
location to create the shape you want. The cube, for example, requires
eighteen vertices, not the eight that you would expect.
If you note the order of vertices in the GL chart above you'll see that all
of them use their vertices slightly differently (in particular you should
make note of the GL_TRIANGLE_STRIP example). Drawing a shape requires that
you keep track of which drawing mode is being used and which order
your vertices are declared in.

If you're thinking: it would be nice if there were an abstraction layer
for this you're thinking right. Enter the mesh, which is really just
an abstraction of the vertex and drawing mode that we started with
but which has the added bonus of managing the draw order for you.
That may seem insignificant at first, but it provides some real benefits
when working with complex geometry.

A very typical usage is something like the following:

~~~~{.cpp}
ofMesh mesh;
for (int y = 0; y < height; y++){
	for (int x = 0; x<width; x++){
		mesh.addVertex(ofPoint(x,y,0)); // make a new vertex
		mesh.addColor(ofFloatColor(0,0,0));  // add a color at that vertex
	}
}
~~~~

Now it's important to make sure that each vertex is correctly connected
with the other vertices around it. This is done using indices, which you
can set up like so:
~~~~{.cpp}
for (int y = 0; y<height-1; y++){
	for (int x=0; x<width-1; x++){
		mesh.addIndex(x+y*width);				// 0
		mesh.addIndex((x+1)+y*width);			// 1
		mesh.addIndex(x+(y+1)*width);			// 10

		mesh.addIndex((x+1)+y*width);			// 1
		mesh.addIndex((x+1)+(y+1)*width);		// 11
		mesh.addIndex(x+(y+1)*width);			// 10
	}
}
~~~~





##Description

An ofMesh represents a set of vertices in 3D spaces, and normals at those points, colors at those points, and texture coordinates at those points. Each of these different properties is stored in a vector.
Vertices are passed to your graphics card and your graphics card fill in the spaces in between them in a processing usually called the rendering pipeline. The rendering pipeline goes more or less like this:

1. Say how you're going to connect all the points.

2. Make some points.

3. Say that you're done making points.

You may be thinking: I'll just make eight vertices and voila: a cube. Not so quick. There's a hitch and that hitch is that the OpenGL renderer has different ways of connecting the vertices that you pass to it and none are as efficient as to only need eight vertices to create a cube.

You've probably seen a version of the following image somewhere before.
![PRIMATIVES](primitives_new-640x269.gif)
Generally you have to create your points to fit the drawing mode that you've selected because of whats called winding. A vertex gets connected to another vertex in the order that the mode does its winding and this means that you might need multiple vertices in a given location to create the shape you want. The cube, for example, requires eighteen vertices, not the eight that you would expect. If you note the order of vertices in the GL chart above you'll see that all of them use their vertices slightly differently (in particular you should make note of the GL_TRIANGLE_STRIP example). Drawing a shape requires that you keep track of which drawing mode is being used and which order your vertices are declared in.

If you're thinking: it would be nice if there were an abstraction layer for this you're thinking right. Enter the mesh, which is really just an abstraction of the vertex and drawing mode that we started with but which has the added bonus of managing the draw order for you. That may seem insignificant at first, but it provides some real benefits when working with complex geometry.

A very typical usage is something like the following:

~~~~{.cpp}
ofMesh mesh;
for (int y = 0; y < height; y++){
	for (int x = 0; x<width; x++){
		mesh.addVertex(ofPoint(x,y,0)); // make a new vertex
		mesh.addColor(ofFloatColor(0,0,0));  // add a color at that vertex
	}
}

// now it's important to make sure that each vertex is correctly connected with the
// other vertices around it. This is done using indices, which you can set up like so:
for (int y = 0; y<height-1; y++){
	for (int x=0; x<width-1; x++){
		mesh.addIndex(x+y*width);				// 0
		mesh.addIndex((x+1)+y*width);			// 1
		mesh.addIndex(x+(y+1)*width);			// 10

		mesh.addIndex((x+1)+y*width);			// 1
		mesh.addIndex((x+1)+(y+1)*width);		// 11
		mesh.addIndex(x+(y+1)*width);			// 10
	}
}
~~~~





##Methods



###void addColor(&c)

<!--
_syntax: addColor(&c)_
_name: addColor_
_returns: void_
_returns_description: _
_parameters: const ofFloatColor &c_
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

This adds a color to the mesh,
the color will be associated with the vertex in the same position.





_description: _

This adds a color to the mesh, the color will be associated with the vertex in the same position.





<!----------------------------------------------------------------------------->

###void addColors(&cols)

<!--
_syntax: addColors(&cols)_
_name: addColors_
_returns: void_
_returns_description: _
_parameters: const vector< ofFloatColor > &cols_
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

This adds colors using a reference to a vector of ofColors.
For each color in the vector, this will put the colors at the corresponding vertex.





_description: _

This adds colors using a reference to a vector of ofColors. For each color in the vector, this will put the colors at the corresponding vertex.





<!----------------------------------------------------------------------------->

###void addColors(*cols, amt)

<!--
_syntax: addColors(*cols, amt)_
_name: addColors_
_returns: void_
_returns_description: _
_parameters: const ofFloatColor *cols, size_t amt_
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

This adds a pointer of colors to the ofMesh instance with the amount passed as the second parameter.





_description: _

This adds a pointer of colors to the ofMesh instance with the amount passed as the second parameter.





<!----------------------------------------------------------------------------->

###void addIndex(i)

<!--
_syntax: addIndex(i)_
_name: addIndex_
_returns: void_
_returns_description: _
_parameters: ofIndexType i_
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Will give you this shape:
![image of basic use of indices](3d/index.jpg)





_description: _

Add an index to the index vector. Each index represents the order of connection for  vertices. This determines the way that the vertices are connected according to the polygon type set in the primitiveMode. It important to note that a particular vertex might be used for several faces and so would be referenced several times in the index vector.
~~~~{.cpp}
    ofMesh mesh;
    mesh.setMode(OF_PRIMITIVE_TRIANGLES);
    mesh.addVertex(ofPoint(0,-200,0));
    mesh.addVertex(ofPoint(200, 0, 0 ));
    mesh.addVertex(ofPoint(-200, 0, 0 ));
    mesh.addVertex(ofPoint(0, 200, 0 ));
    mesh.addIndex(0); //connect the first vertex we made, v0
    mesh.addIndex(1); //to v1
    mesh.addIndex(2); //to v2 to complete the face
    mesh.addIndex(1); //now start a new face beginning with v1
    mesh.addIndex(2); //that is connected to v2
    mesh.addIndex(3); //and we complete the face with v3
~~~~

Will give you this shape:
![image of basic use of indices](index.jpg)





<!----------------------------------------------------------------------------->

###void addIndices(&inds)

<!--
_syntax: addIndices(&inds)_
_name: addIndices_
_returns: void_
_returns_description: _
_parameters: const vector< ofIndexType > &inds_
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

This adds a vector of indices.





_description: _

This adds a vector of indices.





<!----------------------------------------------------------------------------->

###void addIndices(*inds, amt)

<!--
_syntax: addIndices(*inds, amt)_
_name: addIndices_
_returns: void_
_returns_description: _
_parameters: const ofIndexType *inds, size_t amt_
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

This adds indices to the ofMesh by pointing to an array of indices.
The "amt" defines the length of the array.





_description: _

This adds indices to the ofMesh by pointing to an array of indices. The "amt" defines the length of the array.





<!----------------------------------------------------------------------------->

###void addNormal(&n)

<!--
_syntax: addNormal(&n)_
_name: addNormal_
_returns: void_
_returns_description: _
_parameters: const ofVec3f &n_
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Add a normal to the mesh as a 3D vector,
typically perpendicular to the plane of the face. A normal is a vector
that defines how a surface responds to lighting, i.e. how it is lit.
The amount of light reflected by a surface is proportional to the angle
between the light's direction and the normal. The smaller the angle the
brighter the surface will look. See the normalsExample for advice on
computing the normals.
addNormal adds the 3D vector to the end of the list, so you need to
make sure you add normals at the same index of the matching face.





_description: _

Add a normal to the mesh as a 3D vector, typically perpendicular to the plane of the face. A normal is a vector that defines how a surface responds to lighting, i.e. how it is lit. The amount of light reflected by a surface is proportional to the angle between the light's direction and the normal. The smaller the angle the brighter the surface will look. See the normalsExample for advice on computing the normals.
addNormal adds the 3D vector to the end of the list, so you need to make sure you add normals at the same index of the matching face.





<!----------------------------------------------------------------------------->

###void addNormals(&norms)

<!--
_syntax: addNormals(&norms)_
_name: addNormals_
_returns: void_
_returns_description: _
_parameters: const vector< ofVec3f > &norms_
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Add a vector of normals to a mesh,
allowing you to push out many normals at once rather than
adding one at a time. The vector of normals is added after the end of
the current normals list.





_description: _

Add a vector of normals to a mesh, allowing you to push out many normals at once rather than adding one at a time. The vector of normals is added after the end of the current normals list.





<!----------------------------------------------------------------------------->

###void addNormals(*norms, amt)

<!--
_syntax: addNormals(*norms, amt)_
_name: addNormals_
_returns: void_
_returns_description: _
_parameters: const ofVec3f *norms, size_t amt_
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Add an array of normals to the mesh.
Because you are using a pointer to the array you also have to define
the length of the array as an std::size_t (amt). The normals are added at the
end of the current normals list.





_description: _

Add an array of normals to the mesh. Because you are using a pointer to the array you also have to define the length of the array as an int (amt). The normals are added at the end of the current normals list.





<!----------------------------------------------------------------------------->

###void addTexCoord(&t)

<!--
_syntax: addTexCoord(&t)_
_name: addTexCoord_
_returns: void_
_returns_description: _
_parameters: const ofVec2f &t_
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Add a Vec2f representing the texture coordinate.
Because OF uses ARB textures these are in pixels rather than
0-1 normalized coordinates.





_description: _

Add a Vec2f representing the texture coordinate. Because OF uses ARB textures these are in pixels rather than 0-1 normalized coordinates.





<!----------------------------------------------------------------------------->

###void addTexCoords(&tCoords)

<!--
_syntax: addTexCoords(&tCoords)_
_name: addTexCoords_
_returns: void_
_returns_description: _
_parameters: const vector< ofVec2f > &tCoords_
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Add a vector of texture coordinates to a mesh,
allowing you to push out many at once rather than adding one at a time.
The vector of texture coordinates is added after the end of the current
texture coordinates list.





_description: _

Add a vector of texture coordinates to a mesh, allowing you to push out many at once rather than adding one at a time. The vector of texture coordinates is added after the end of the current texture coordinates list.





<!----------------------------------------------------------------------------->

###void addTexCoords(*tCoords, amt)

<!--
_syntax: addTexCoords(*tCoords, amt)_
_name: addTexCoords_
_returns: void_
_returns_description: _
_parameters: const ofVec2f *tCoords, size_t amt_
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

 Add an array of texture coordinates to the mesh.
Because you are using a pointer to the array you also have to define
the length of the array as an std::size_t (amt).
The texture coordinates are added at the end of the current texture
coordinates list.





_description: _

Add an array of texture coordinates to the mesh. Because you are using a pointer to the array you also have to define the length of the array as an int (amt). The texture coordinates are added at the end of the current texture coordinates list.





<!----------------------------------------------------------------------------->

###void addTriangle(index1, index2, index3)

<!--
_syntax: addTriangle(index1, index2, index3)_
_name: addTriangle_
_returns: void_
_returns_description: _
_parameters: ofIndexType index1, ofIndexType index2, ofIndexType index3_
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Adding a triangle means using three of the vertices that have already been added to create a triangle.
This is an easy way to create triangles in the mesh. The indices refer to the index of the vertex in the vector of vertices.





_description: _

Adding a triangle means using three of the vertices that have already been added to create a triangle. This is an easy way to create triangles in the mesh. The indices refer to the index of the vertex in the vector of vertices.





<!----------------------------------------------------------------------------->

###void addVertex(&v)

<!--
_syntax: addVertex(&v)_
_name: addVertex_
_returns: void_
_returns_description: _
_parameters: const ofVec3f &v_
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Add a new vertex at the end of the current list of vertices.
It is important to remember that the order the vertices are added to
the list determines how they link they form the polygons and strips
(assuming you do not change their indeces). See the ofMesh class
description for details.





_description: _

Add a new vertex at the end of the current list of vertices. It is important to remember that the order the vertices are added to the list determines how they link they form the polygons and strips (assuming you do not change their indeces). See the ofMesh class description for details.





<!----------------------------------------------------------------------------->

###void addVertices(&verts)

<!--
_syntax: addVertices(&verts)_
_name: addVertices_
_returns: void_
_returns_description: _
_parameters: const vector< ofVec3f > &verts_
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Add a vector of vertices to a mesh, allowing you to push out
many at once rather than adding one at a time. The vector of vertices
is added after the end of the current vertices list.





_description: _

Add a vector of vertices to a mesh, allowing you to push out many at once rather than adding one at a time. The vector of vertices is added after the end of the current vertices list.





<!----------------------------------------------------------------------------->

###void addVertices(*verts, amt)

<!--
_syntax: addVertices(*verts, amt)_
_name: addVertices_
_returns: void_
_returns_description: _
_parameters: const ofVec3f *verts, size_t amt_
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Add an array of vertices to the mesh.
Because you are using a pointer to the array you also have to define
the length of the array as an int (amt). The vertices are added at the
end of the current vertices list.





_description: _

Add an array of vertices to the mesh. Because you are using a pointer to the array you also have to define the length of the array as an int (amt). The vertices are added at the end of the current vertices list.





<!----------------------------------------------------------------------------->

###void append(&mesh)

<!--
_syntax: append(&mesh)_
_name: append_
_returns: void_
_returns_description: _
_parameters: const ofMesh &mesh_
_access: public_
_version_started: 0073_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Add the vertices, normals, texture coordinates and indices of one mesh onto another mesh.
Everything from the referenced mesh is simply added at the end
of the current mesh's lists.





_description: _

Add the vertices, normals, texture coordinates and indices of one mesh onto another mesh. Everything from the referenced mesh is simply added at the end of the current mesh's lists.





<!----------------------------------------------------------------------------->

###ofMesh axis(size)

<!--
_syntax: axis(size)_
_name: axis_
_returns: ofMesh_
_returns_description: _
_parameters: float size_
_access: public_
_version_started: 0.8.0_
_version_deprecated: _
_summary: _
_constant: False_
_static: True_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: an ofMesh representing an XYZ coordinate system.





_description: _







<!----------------------------------------------------------------------------->

###ofMesh box(width, height, depth, resX = 2, resY = 2, resZ = 2)

<!--
_syntax: box(width, height, depth, resX = 2, resY = 2, resZ = 2)_
_name: box_
_returns: ofMesh_
_returns_description: _
_parameters: float width, float height, float depth, int resX=2, int resY=2, int resZ=2_
_access: public_
_version_started: 0073_
_version_deprecated: _
_summary: _
_constant: False_
_static: True_
_visible: True_
_advanced: False_
-->

_inlined_description: _

A helper method that returns a box made of triangles.
The resolution settings for the width and height are optional
(they are both set at a default of 2 triangles per side).
~~~~{.cpp}
ofMesh mesh;
mesh = ofMesh::box(200.0, 200.0, 200.0);
~~~~

![image of a simple box](3d/box.jpg)





_description: _

A helper method that returns a box made of triangles. The resolution settings for the width and height are optional (they are both set at a default of 2 triangles per side).
~~~~{.cpp}
ofMesh mesh;
mesh = ofMesh::box(200.0, 200.0, 200.0);
~~~~

![image of a simple box](box.jpg)





<!----------------------------------------------------------------------------->

###void clear()

<!--
_syntax: clear()_
_name: clear_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Removes all the vertices, colors, and indices from the mesh.





_description: _

This removes all the vertices, colors, and indices from the mesh.





<!----------------------------------------------------------------------------->

###void clearColors()

<!--
_syntax: clearColors()_
_name: clearColors_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Clear all the colors.





_description: _

Clear all the colors.





<!----------------------------------------------------------------------------->

###void clearIndices()

<!--
_syntax: clearIndices()_
_name: clearIndices_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Remove all the indices of the mesh.
This means that your mesh will be a point cloud.





_description: _

Remove all the indices of the mesh. This means that your mesh will be a point cloud.





<!----------------------------------------------------------------------------->

###void clearNormals()

<!--
_syntax: clearNormals()_
_name: clearNormals_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Remove all the normals.





_description: _

Remove all the normals.





<!----------------------------------------------------------------------------->

###void clearTexCoords()

<!--
_syntax: clearTexCoords()_
_name: clearTexCoords_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

 Clear all the texture coordinates.





_description: _

Clear all the texture coordinates.





<!----------------------------------------------------------------------------->

###void clearVertices()

<!--
_syntax: clearVertices()_
_name: clearVertices_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Removes all the vertices.





_description: _

Removes all the vertices.





<!----------------------------------------------------------------------------->

###ofMesh cone(radius, height, radiusSegments = 12, heightSegments = 6, capSegments = 2, mode = OF_PRIMITIVE_TRIANGLE_STRIP)

<!--
_syntax: cone(radius, height, radiusSegments = 12, heightSegments = 6, capSegments = 2, mode = OF_PRIMITIVE_TRIANGLE_STRIP)_
_name: cone_
_returns: ofMesh_
_returns_description: _
_parameters: float radius, float height, int radiusSegments=12, int heightSegments=6, int capSegments=2, ofPrimitiveMode mode=OF_PRIMITIVE_TRIANGLE_STRIP_
_access: public_
_version_started: 0073_
_version_deprecated: _
_summary: _
_constant: False_
_static: True_
_visible: True_
_advanced: False_
-->

_inlined_description: _

A helper method that returns a cone made of triangles.
The resolution settings for the radius, height, and cap are optional
(they are set at a default of 12 segments around the radius, 6 segments
in the height, and 2 on the cap). The only valid modes are the default
OF_PRIMITIVE_TRIANGLE_STRIP and OF_PRIMITIVE_TRIANGLES.
~~~~{.cpp}
ofMesh mesh;
mesh = ofMesh::cone(100.0, 200.0);
~~~~

![image of a simple cone](3d/cone.jpg)





_description: _

A helper method that returns a cone made of triangles. The resolution settings for the radius, height, and cap are optional (they are set at a default of 12 segments around the radius, 6 segments in the height, and 2 on the cap). The only valid modes are the default OF_PRIMITIVE_TRIANGLE_STRIP and OF_PRIMITIVE_TRIANGLES.
~~~~{.cpp}
ofMesh mesh;
mesh = ofMesh::cone(100.0, 200.0);
~~~~

![image of a simple cone](cone.jpg)





<!----------------------------------------------------------------------------->

###ofMesh cylinder(radius, height, radiusSegments = 12, heightSegments = 6, numCapSegments = 2, bCapped = true, mode = OF_PRIMITIVE_TRIANGLE_STRIP)

<!--
_syntax: cylinder(radius, height, radiusSegments = 12, heightSegments = 6, numCapSegments = 2, bCapped = true, mode = OF_PRIMITIVE_TRIANGLE_STRIP)_
_name: cylinder_
_returns: ofMesh_
_returns_description: _
_parameters: float radius, float height, int radiusSegments=12, int heightSegments=6, int numCapSegments=2, bool bCapped=true, ofPrimitiveMode mode=OF_PRIMITIVE_TRIANGLE_STRIP_
_access: public_
_version_started: 0073_
_version_deprecated: _
_summary: _
_constant: False_
_static: True_
_visible: True_
_advanced: False_
-->

_inlined_description: _

	A helper method that returns a cylinder made of triangles.
The resolution settings for the radius, height, and cap are optional
(they are set at a default of 12 segments around the radius, 6 segments
in the height, and 2 on the cap). You have the option to cap the
cylinder or not. The only valid modes are the default
OF_PRIMITIVE_TRIANGLE_STRIP and OF_PRIMITIVE_TRIANGLES.
	~~~~{.cpp}
	ofMesh mesh;
	mesh = ofMesh::cylinder(100.0, 200.0);
	~~~~

	![image of a simple cylinder](3d/cylinder.jpg)





_description: _

A helper method that returns a cylinder made of triangles. The resolution settings for the radius, height, and cap are optional (they are set at a default of 12 segments around the radius, 6 segments in the height, and 2 on the cap). You have the option to cap the cylinder or not. The only valid modes are the default OF_PRIMITIVE_TRIANGLE_STRIP and OF_PRIMITIVE_TRIANGLES.
~~~~{.cpp}
ofMesh mesh;
mesh = ofMesh::cylinder(100.0, 200.0);
~~~~

![image of a simple cylinder](cylinder.jpg)





<!----------------------------------------------------------------------------->

###void disableColors()

<!--
_syntax: disableColors()_
_name: disableColors_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0071_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Disable mesh colors.
Use enableColors() to turn colors back on.





_description: _

Disable mesh colors. Use enableColors() to turn colors back on.





<!----------------------------------------------------------------------------->

###void disableIndices()

<!--
_syntax: disableIndices()_
_name: disableIndices_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Disable mesh indices.
Use enableIndices() to turn indices back on.





_description: _

Disable mesh indices. Use enableIndices() to turn indices back on.





<!----------------------------------------------------------------------------->

###void disableNormals()

<!--
_syntax: disableNormals()_
_name: disableNormals_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0071_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Disable mesh normals.
Use enableNormals() to turn normals back on.





_description: _

Disable mesh normals. Use enableNormals() to turn normals back on.





<!----------------------------------------------------------------------------->

###void disableTextures()

<!--
_syntax: disableTextures()_
_name: disableTextures_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0071_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Disable mesh textures.
Use enableTextures() to turn textures back on.





_description: _

Disable mesh textures. Use enableTextures() to turn textures back on.





<!----------------------------------------------------------------------------->

###void draw()

<!--
_syntax: draw()_
_name: draw_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

This draws the mesh using its primitive type, meaning that if
you set them up to be triangles, this will draw the triangles.





_description: _

This draws the mesh using its primitive type, meaning that if you set them up to be triangles, this will draw the triangles.





<!----------------------------------------------------------------------------->

###void draw(renderType)

<!--
_syntax: draw(renderType)_
_name: draw_
_returns: void_
_returns_description: _
_parameters: ofPolyRenderMode renderType_
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

This draws the mesh using a defined renderType,
overriding the renderType defined with setMode().





_description: _

This draws the mesh using a defined renderType, overriding the renderType defined with setMode().





<!----------------------------------------------------------------------------->

###void drawFaces()

<!--
_syntax: drawFaces()_
_name: drawFaces_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

This draws the mesh as faces, meaning that you'll have a collection of faces.





_description: _

This draws the mesh as faces, meaning that you'll have a collection of faces.





<!----------------------------------------------------------------------------->

###void drawVertices()

<!--
_syntax: drawVertices()_
_name: drawVertices_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

This allows you draw just the vertices, meaning that you'll have a point cloud.





_description: _

This allows you draw just the vertices, meaning that you'll have a point cloud.





<!----------------------------------------------------------------------------->

###void drawWireframe()

<!--
_syntax: drawWireframe()_
_name: drawWireframe_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

This draws the mesh as GL_LINES, meaning that you'll have a wireframe.





_description: _

This draws the mesh as GL_LINES, meaning that you'll have a wireframe.





<!----------------------------------------------------------------------------->

###void enableColors()

<!--
_syntax: enableColors()_
_name: enableColors_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0071_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Enable mesh colors.
Use disableColors() to turn colors off.
Colors are enabled by default when they are added to the mesh.





_description: _

Enable mesh colors. Use disableColors() to turn colors off. Colors are enabled by default when they are added to the mesh.





<!----------------------------------------------------------------------------->

###void enableIndices()

<!--
_syntax: enableIndices()_
_name: enableIndices_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Enable mesh indices.
Use disableIndices() to turn indices off.
Indices are enabled by default when they are added to the mesh.





_description: _

Enable mesh indices. Use disableIndices() to turn indices off. Indices are enabled by default when they are added to the mesh.





<!----------------------------------------------------------------------------->

###void enableNormals()

<!--
_syntax: enableNormals()_
_name: enableNormals_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0071_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Enable mesh normals.
Use disableNormals() to turn normals off.
Normals are enabled by default when they are added to the mesh.





_description: _

Enable mesh normals. Use disableNormals() to turn normals off. Normals are enabled by default when they are added to the mesh.





<!----------------------------------------------------------------------------->

###void enableTextures()

<!--
_syntax: enableTextures()_
_name: enableTextures_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0071_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Enable mesh textures.
Use disableTextures() to turn textures off.
Textures are enabled by default when they are added to the mesh.





_description: _

Enable mesh textures. Use disableTextures() to turn textures off. Textures are enabled by default when they are added to the mesh.





<!----------------------------------------------------------------------------->

###ofVec3f getCentroid()

<!--
_syntax: getCentroid()_
_name: getCentroid_
_returns: ofVec3f_
_returns_description: _
_parameters: _
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: a ofVec3f defining the centroid of all the vetices in the mesh.





_description: _

Returns a ofVec3f defining the centroid of all the vetices in the mesh.





<!----------------------------------------------------------------------------->

###ofFloatColor getColor(i)

<!--
_syntax: getColor(i)_
_name: getColor_
_returns: ofFloatColor_
_returns_description: _
_parameters: ofIndexType i_
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Get the color at the index in the colors vector.

Returns: the color at the index in the colors vector.





_description: _

Returns the color at the index in the colors vector.





<!----------------------------------------------------------------------------->

###vector< ofFloatColor > & getColors()

<!--
_syntax: getColors()_
_name: getColors_
_returns: vector< ofFloatColor > &_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0.8.0_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Use this if you plan to change the colors as part of this call as it will force a reset of the cache.

Returns: the vector that contains all of the colors of the mesh, if it has any.





_description: _

Returns the vector that contains all of the colors of the mesh, if it has any. Use this if you plan to change the colors as part of this call as it will force a reset of the cache.





<!----------------------------------------------------------------------------->

###const vector< ofFloatColor > & getColors()

<!--
_syntax: getColors()_
_name: getColors_
_returns: const vector< ofFloatColor > &_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: the vector that contains all of the colors of the mesh, if it has any. (read only)





_description: _

Returns the vector that contains all of the colors of the mesh, if it has any. (read only)





<!----------------------------------------------------------------------------->

###ofFloatColor * getColorsPointer()

<!--
_syntax: getColorsPointer()_
_name: getColorsPointer_
_returns: ofFloatColor *_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0.8.0_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Use this if you plan to change the colors as part of this call as it will force a reset of the cache.

Returns: a pointer that contains all of the colors of the mesh, if it has any.





_description: _

Returns a pointer that contains all of the colors of the mesh, if it has any. Use this if you plan to change the colors as part of this call as it will force a reset of the cache.





<!----------------------------------------------------------------------------->

###const ofFloatColor * getColorsPointer()

<!--
_syntax: getColorsPointer()_
_name: getColorsPointer_
_returns: const ofFloatColor *_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: a pointer that contains all of the colors of the mesh, if it has any. (read only)





_description: _

Returns a pointer that contains all of the colors of the mesh, if it has any. (read only)





<!----------------------------------------------------------------------------->

###ofMeshFace getFace(faceId)

<!--
_syntax: getFace(faceId)_
_name: getFace_
_returns: ofMeshFace_
_returns_description: _
_parameters: ofIndexType faceId_
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: the vector that contains all of the faces of the mesh. This isn't currently implemented.





_description: _

Returns the vector that contains all of the faces of the mesh. This isn't currently implemented.





<!----------------------------------------------------------------------------->

###vector< ofVec3f > getFaceNormals(perVetex = false)

<!--
_syntax: getFaceNormals(perVetex = false)_
_name: getFaceNormals_
_returns: vector< ofVec3f >_
_returns_description: _
_parameters: bool perVetex=false_
_access: public_
_version_started: 0073_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Get normals for each face
As a default it only calculates the normal for the face as a whole but
by setting (perVertex = true) it will return the same normal value for
each of the three vertices making up a face.

Returns: a vector containing the calculated normals of each face in the mesh.





_description: _

Returns a vector containing the calculated normals of each face in the mesh. As a default it only calculates the normal for the face as a whole but by setting (perVertex = true) it will return the same normal value for each of the three vertices making up a face.





<!----------------------------------------------------------------------------->

###ofIndexType getIndex(i)

<!--
_syntax: getIndex(i)_
_name: getIndex_
_returns: ofIndexType_
_returns_description: _
_parameters: ofIndexType i_
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: the index from the index vector. Each index represents the index of the vertex in the vertices vector. This determines the way that the vertices are connected into the polgoynon type set in the primitiveMode.





_description: _

Returns the index from the index vector. Each index represents the index of the vertex in the vertices vector. This determines the way that the vertices are connected into the polgoynon type set in the primitiveMode.





<!----------------------------------------------------------------------------->

###ofIndexType * getIndexPointer()

<!--
_syntax: getIndexPointer()_
_name: getIndexPointer_
_returns: ofIndexType *_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0.8.0_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: a pointer to the indices that the mesh contains.





_description: _

Returns a pointer to the indices that the mesh contains.





<!----------------------------------------------------------------------------->

###const ofIndexType * getIndexPointer()

<!--
_syntax: getIndexPointer()_
_name: getIndexPointer_
_returns: const ofIndexType *_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: a pointer to the indices that the mesh contains.





_description: _

Returns a pointer to the indices that the mesh contains.





<!----------------------------------------------------------------------------->

###vector< ofIndexType > & getIndices()

<!--
_syntax: getIndices()_
_name: getIndices_
_returns: vector< ofIndexType > &_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0.8.0_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Use this if you plan to change the indices as part of this call as it
will force a reset of the cache.

Returns: the vector that contains all of the indices of the mesh, if it has any.





_description: _

Returns the vector that contains all of the indices of the mesh, if it has any. Use this if you plan to change the indices as part of this call as it will force a reset of the cache.





<!----------------------------------------------------------------------------->

###const vector< ofIndexType > & getIndices()

<!--
_syntax: getIndices()_
_name: getIndices_
_returns: const vector< ofIndexType > &_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: the vector that contains all of the indices of the mesh, if it has any. (read only)





_description: _

Returns the vector that contains all of the indices of the mesh, if it has any. (read only)





<!----------------------------------------------------------------------------->

###ofMesh getMeshForIndices(startIndex, endIndex)

<!--
_syntax: getMeshForIndices(startIndex, endIndex)_
_name: getMeshForIndices_
_returns: ofMesh_
_returns_description: _
_parameters: ofIndexType startIndex, ofIndexType endIndex_
_access: public_
_version_started: 0073_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

The new mesh includes the mesh mode, colors, textures, and normals of the original mesh (assuming any were added).

Returns: a mesh made up of a range of indices from startIndex to the endIndex.





_description: _

Returns a mesh made up of a range of indices from startIndex to the endIndex. The new mesh includes the mesh mode, colors, textures, and normals of the original mesh (assuming any were added).





<!----------------------------------------------------------------------------->

###ofMesh getMeshForIndices(startIndex, endIndex, startVertIndex, endVertIndex)

<!--
_syntax: getMeshForIndices(startIndex, endIndex, startVertIndex, endVertIndex)_
_name: getMeshForIndices_
_returns: ofMesh_
_returns_description: _
_parameters: ofIndexType startIndex, ofIndexType endIndex, ofIndexType startVertIndex, ofIndexType endVertIndex_
_access: public_
_version_started: 0073_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###ofPrimitiveMode getMode()

<!--
_syntax: getMode()_
_name: getMode_
_returns: ofPrimitiveMode_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

\
Returns: the primitive mode that the mesh is using.





_description: _

Returns the primitive mode that the mesh is using.





<!----------------------------------------------------------------------------->

###ofVec3f getNormal(i)

<!--
_syntax: getNormal(i)_
_name: getNormal_
_returns: ofVec3f_
_returns_description: _
_parameters: ofIndexType i_
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

\
Returns: the normal at the index in the normals vector.





_description: _

Returns the normal at the index in the normals vector.





<!----------------------------------------------------------------------------->

###vector< ofVec3f > & getNormals()

<!--
_syntax: getNormals()_
_name: getNormals_
_returns: vector< ofVec3f > &_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0.8.0_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Use this if you plan to change the normals as part of this call as it
will force a reset of the cache.

Returns: the vector that contains all of the normals of the mesh,
if it has any.





_description: _

Returns the vector that contains all of the normals of the mesh, if it has any. Use this if you plan to change the normals as part of this call as it will force a reset of the cache.





<!----------------------------------------------------------------------------->

###const vector< ofVec3f > & getNormals()

<!--
_syntax: getNormals()_
_name: getNormals_
_returns: const vector< ofVec3f > &_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: the vector that contains all of the normals of the mesh, if
it has any. (read only)





_description: _

Returns the vector that contains all of the normals of the mesh, if it has any. (read only)





<!----------------------------------------------------------------------------->

###ofVec3f * getNormalsPointer()

<!--
_syntax: getNormalsPointer()_
_name: getNormalsPointer_
_returns: ofVec3f *_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0.8.0_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: a pointer to the normals that the mesh contains.





_description: _

Returns a pointer to the normals that the mesh contains.





<!----------------------------------------------------------------------------->

###const ofVec3f * getNormalsPointer()

<!--
_syntax: getNormalsPointer()_
_name: getNormalsPointer_
_returns: const ofVec3f *_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: a pointer to the normals that the mesh contains.





_description: _

Returns a pointer to the normals that the mesh contains.





<!----------------------------------------------------------------------------->

###size_t getNumColors()

<!--
_syntax: getNumColors()_
_name: getNumColors_
_returns: size_t_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: the size of the colors vector for the mesh.
This will tell you how many colors are contained in the mesh.





_description: _

Returns the size of the colors vector for the mesh. This will tell you how many colors are contained in the mesh.





<!----------------------------------------------------------------------------->

###size_t getNumIndices()

<!--
_syntax: getNumIndices()_
_name: getNumIndices_
_returns: size_t_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

This will tell you how many indices are contained in the mesh.

Returns: the size of the indices vector for the mesh.





_description: _

Returns the size of the indices vector for the mesh. This will tell you how many indices are contained in the mesh.





<!----------------------------------------------------------------------------->

###size_t getNumNormals()

<!--
_syntax: getNumNormals()_
_name: getNumNormals_
_returns: size_t_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

This will tell you how many normals are contained in the mesh.

Returns: the size of the normals vector for the mesh.





_description: _

Returns the size of the normals vector for the mesh. This will tell you how many normals are contained in the mesh.





<!----------------------------------------------------------------------------->

###size_t getNumTexCoords()

<!--
_syntax: getNumTexCoords()_
_name: getNumTexCoords_
_returns: size_t_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

This will tell you how many texture coordinates are contained in the mesh.

Returns: the size of the texture coordinates vector for the mesh.





_description: _

Returns the size of the texture coordinates vector for the mesh. This will tell you how many texture coordinates are contained in the mesh.





<!----------------------------------------------------------------------------->

###size_t getNumVertices()

<!--
_syntax: getNumVertices()_
_name: getNumVertices_
_returns: size_t_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: the size of the vertices vector for the mesh.
This will tell you how many vertices are contained in the mesh.





_description: _

Returns the size of the vertices vector for the mesh. This will tell you how many vertices are contained in the mesh.





<!----------------------------------------------------------------------------->

###ofVec2f getTexCoord(i)

<!--
_syntax: getTexCoord(i)_
_name: getTexCoord_
_returns: ofVec2f_
_returns_description: _
_parameters: ofIndexType i_
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: the Vec2f representing the texture coordinate.
Because OF uses ARB textures these are in pixels rather than
0-1 normalized coordinates.





_description: _

Returns the Vec2f representing the texture coordinate. Because OF uses ARB textures these are in pixels rather than 0-1 normalized coordinates.





<!----------------------------------------------------------------------------->

###vector< ofVec2f > & getTexCoords()

<!--
_syntax: getTexCoords()_
_name: getTexCoords_
_returns: vector< ofVec2f > &_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0.8.0_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Get a vector representing the texture coordinates of the mesh
Because OF uses ARB textures these are in pixels rather than 0-1 normalized coordinates.
Use this if you plan to change the texture coordinates as part of this
call as it will force a reset of the cache.

Returns: a vector of Vec2f representing the texture coordinates for the whole mesh.





_description: _

Returns a vector of Vec2f representing the texture coordinates for the whole mesh. Because OF uses ARB textures these are in pixels rather than 0-1 normalized coordinates. Use this if you plan to change the texture coordinates as part of this call as it will force a reset of the cache.





<!----------------------------------------------------------------------------->

###const vector< ofVec2f > & getTexCoords()

<!--
_syntax: getTexCoords()_
_name: getTexCoords_
_returns: const vector< ofVec2f > &_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Because OF uses ARB textures these are in pixels rather than 0-1 normalized coordinates.

Returns: a vector of Vec2f representing the texture coordinates for the whole mesh. (read only)





_description: _

Returns a vector of Vec2f representing the texture coordinates for the whole mesh. Because OF uses ARB textures these are in pixels rather than 0-1 normalized coordinates. (read only)





<!----------------------------------------------------------------------------->

###ofVec2f * getTexCoordsPointer()

<!--
_syntax: getTexCoordsPointer()_
_name: getTexCoordsPointer_
_returns: ofVec2f *_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0.8.0_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: a pointer to the texture coords that the mesh contains.





_description: _

Returns a pointer to the texture coords that the mesh contains.





<!----------------------------------------------------------------------------->

###const ofVec2f * getTexCoordsPointer()

<!--
_syntax: getTexCoordsPointer()_
_name: getTexCoordsPointer_
_returns: const ofVec2f *_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Get a pointer to the ofVec2f texture coordinates that the mesh contains.





_description: _

Get a pointer to the ofVec2f texture coordinates that the mesh contains.





<!----------------------------------------------------------------------------->

###const vector< ofMeshFace > & getUniqueFaces()

<!--
_syntax: getUniqueFaces()_
_name: getUniqueFaces_
_returns: const vector< ofMeshFace > &_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0073_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: the mesh as a vector of unique ofMeshFaces
a list of triangles that do not share vertices or indices





_description: _

Returns the mesh as a vector of unique ofMeshFaces.





<!----------------------------------------------------------------------------->

###ofVec3f getVertex(i)

<!--
_syntax: getVertex(i)_
_name: getVertex_
_returns: ofVec3f_
_returns_description: _
_parameters: ofIndexType i_
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: the vertex at the index.





_description: _

Returns the vertex at the index.





<!----------------------------------------------------------------------------->

###vector< ofVec3f > & getVertices()

<!--
_syntax: getVertices()_
_name: getVertices_
_returns: vector< ofVec3f > &_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0.8.0_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: the vector that contains all of the vertices of the mesh.





_description: _

Returns the vector that contains all of the vertices of the mesh.





<!----------------------------------------------------------------------------->

###const vector< ofVec3f > & getVertices()

<!--
_syntax: getVertices()_
_name: getVertices_
_returns: const vector< ofVec3f > &_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: the vector that contains all of the vertices of the mesh.





_description: _

Returns the vector that contains all of the vertices of the mesh.





<!----------------------------------------------------------------------------->

###ofVec3f * getVerticesPointer()

<!--
_syntax: getVerticesPointer()_
_name: getVerticesPointer_
_returns: ofVec3f *_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0.8.0_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: a pointer to the vertices that the mesh contains.





_description: _

Returns a pointer to the vertices that the mesh contains.





<!----------------------------------------------------------------------------->

###const ofVec3f * getVerticesPointer()

<!--
_syntax: getVerticesPointer()_
_name: getVerticesPointer_
_returns: const ofVec3f *_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: a pointer to the vertices that the mesh contains.





_description: _

Returns a pointer to the vertices that the mesh contains.





<!----------------------------------------------------------------------------->

###bool hasColors()

<!--
_syntax: hasColors()_
_name: hasColors_
_returns: bool_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

/returns Whether the mesh has any colors.





_description: _

Whether the mesh has any colors.





<!----------------------------------------------------------------------------->

###bool hasIndices()

<!--
_syntax: hasIndices()_
_name: hasIndices_
_returns: bool_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

/returns Whether the mesh has any indices assigned to it.





_description: _

Whether the mesh has any indices assigned to it.





<!----------------------------------------------------------------------------->

###bool hasNormals()

<!--
_syntax: hasNormals()_
_name: hasNormals_
_returns: bool_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

/returnsWhether the mesh has any normals.





_description: _

Whether the mesh has any normals.





<!----------------------------------------------------------------------------->

###bool hasTexCoords()

<!--
_syntax: hasTexCoords()_
_name: hasTexCoords_
_returns: bool_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

/returns Whether the mesh has any textures assigned to it.





_description: _

Whether the mesh has any textures assigned to it.





<!----------------------------------------------------------------------------->

###bool hasVertices()

<!--
_syntax: hasVertices()_
_name: hasVertices_
_returns: bool_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: Whether the mesh has any vertices.





_description: _

Whether the mesh has any vertices.





<!----------------------------------------------------------------------------->

###bool haveColorsChanged()

<!--
_syntax: haveColorsChanged()_
_name: haveColorsChanged_
_returns: bool_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: If the colors of the mesh have changed, been added or removed.





_description: _

If the colors of the mesh have changed, been added or removed.





<!----------------------------------------------------------------------------->

###bool haveIndicesChanged()

<!--
_syntax: haveIndicesChanged()_
_name: haveIndicesChanged_
_returns: bool_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: If the indices of the mesh have changed, been added or removed.





_description: _

If the indices of the mesh have changed, been added or removed.





<!----------------------------------------------------------------------------->

###bool haveNormalsChanged()

<!--
_syntax: haveNormalsChanged()_
_name: haveNormalsChanged_
_returns: bool_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: If the normals of the mesh have changed, been added or removed.





_description: _

If the normals of the mesh have changed, been added or removed.





<!----------------------------------------------------------------------------->

###bool haveTexCoordsChanged()

<!--
_syntax: haveTexCoordsChanged()_
_name: haveTexCoordsChanged_
_returns: bool_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: If the texture coords of the mesh have changed, been added or removed.





_description: _

If the texture coords of the mesh have changed, been added or removed.





<!----------------------------------------------------------------------------->

###bool haveVertsChanged()

<!--
_syntax: haveVertsChanged()_
_name: haveVertsChanged_
_returns: bool_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Returns: If the vertices of the mesh have changed, been added or removed.





_description: _

If the vertices of the mesh have changed, been added or removed.





<!----------------------------------------------------------------------------->

###ofMesh icosahedron(radius)

<!--
_syntax: icosahedron(radius)_
_name: icosahedron_
_returns: ofMesh_
_returns_description: _
_parameters: float radius_
_access: public_
_version_started: 0073_
_version_deprecated: _
_summary: _
_constant: False_
_static: True_
_visible: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###ofMesh icosphere(radius, iterations)

<!--
_syntax: icosphere(radius, iterations)_
_name: icosphere_
_returns: ofMesh_
_returns_description: _
_parameters: float radius, size_t iterations_
_access: public_
_version_started: 0073_
_version_deprecated: _
_summary: _
_constant: False_
_static: True_
_visible: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###void load(path)

<!--
_syntax: load(path)_
_name: load_
_returns: void_
_returns_description: _
_parameters: string path_
_access: public_
_version_started: 0071_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Loads a mesh from a file located at the provided path into the mesh.
This will replace any existing data within the mesh.

It expects that the file will be in the [PLY Format](http://en.wikipedia.org/wiki/PLY_(file_format)).
It will only load meshes saved in the PLY ASCII format; the binary format is not supported.





_description: _

Loads a mesh from a file located at the provided path into the mesh.
This will replace any existing data within the mesh.

It expects that the file will be in the [PLY Format](http://en.wikipedia.org/wiki/PLY_(file_format)).
It will only load meshes saved in the PLY ASCII format; the binary format is not supported.





<!----------------------------------------------------------------------------->

###void mergeDuplicateVertices()

<!--
_syntax: mergeDuplicateVertices()_
_name: mergeDuplicateVertices_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0073_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

### ofMesh()

<!--
_syntax: ofMesh()_
_name: ofMesh_
_returns: _
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

This creates the mesh,
using OF_PRIMITIVE_TRIANGLES without any initial vertices.





_description: _

This creates the mesh, using OF_PRIMITIVE_TRIANGLES and without any initial vertices.





<!----------------------------------------------------------------------------->

### ofMesh(mode, &verts)

<!--
_syntax: ofMesh(mode, &verts)_
_name: ofMesh_
_returns: _
_returns_description: _
_parameters: ofPrimitiveMode mode, const vector< ofVec3f > &verts_
_access: public_
_version_started: 007_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

This allows to you to use one of the other ofPrimitiveModes:
OF_PRIMITIVE_TRIANGLES, OF_PRIMITIVE_TRIANGLE_STRIP,
OF_PRIMITIVE_TRIANGLE_FAN, OF_PRIMITIVE_LINES, OF_PRIMITIVE_LINE_STRIP,
OF_PRIMITIVE_LINE_LOOP, OF_PRIMITIVE_POINTS.
See [ofGLUtils](../gl/ofGLUtils.htm) for more information on these types.





_description: _

This allows to you to use one of the other ofPrimitiveModes: OF_PRIMITIVE_TRIANGLES, OF_PRIMITIVE_TRIANGLE_STRIP, OF_PRIMITIVE_TRIANGLE_FAN, OF_PRIMITIVE_LINES, OF_PRIMITIVE_LINE_STRIP, OF_PRIMITIVE_LINE_LOOP, OF_PRIMITIVE_POINTS. See [ofGLUtils](../gl/ofGLUtils.htm) for more information on these types.





<!----------------------------------------------------------------------------->

###ofMesh plane(width, height, columns = 2, rows = 2, mode = OF_PRIMITIVE_TRIANGLE_STRIP)

<!--
_syntax: plane(width, height, columns = 2, rows = 2, mode = OF_PRIMITIVE_TRIANGLE_STRIP)_
_name: plane_
_returns: ofMesh_
_returns_description: _
_parameters: float width, float height, int columns=2, int rows=2, ofPrimitiveMode mode=OF_PRIMITIVE_TRIANGLE_STRIP_
_access: public_
_version_started: 0073_
_version_deprecated: _
_summary: _
_constant: False_
_static: True_
_visible: True_
_advanced: False_
-->

_inlined_description: _

\}
\name Primitive constructor helper methods
\{





_description: _







<!----------------------------------------------------------------------------->

###void removeColor(index)

<!--
_syntax: removeColor(index)_
_name: removeColor_
_returns: void_
_returns_description: _
_parameters: ofIndexType index_
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Remove a color at the index in the colors vector.





_description: _

Remove a color at the index in the colors vector.





<!----------------------------------------------------------------------------->

###void removeIndex(index)

<!--
_syntax: removeIndex(index)_
_name: removeIndex_
_returns: void_
_returns_description: _
_parameters: ofIndexType index_
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Removes an index.





_description: _

Removes an index.





<!----------------------------------------------------------------------------->

###void removeNormal(index)

<!--
_syntax: removeNormal(index)_
_name: removeNormal_
_returns: void_
_returns_description: _
_parameters: ofIndexType index_
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Remove a normal.





_description: _

Remove a normal.





<!----------------------------------------------------------------------------->

###void removeTexCoord(index)

<!--
_syntax: removeTexCoord(index)_
_name: removeTexCoord_
_returns: void_
_returns_description: _
_parameters: ofIndexType index_
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

 Remove a Vec2f representing the texture coordinate.





_description: _

Remove a Vec2f representing the texture coordinate.





<!----------------------------------------------------------------------------->

###void removeVertex(index)

<!--
_syntax: removeVertex(index)_
_name: removeVertex_
_returns: void_
_returns_description: _
_parameters: ofIndexType index_
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Removes the vertex at the index in the vector.





_description: _

Removes the vertex at the index in the vector.





<!----------------------------------------------------------------------------->

###void save(path, useBinary = false)

<!--
_syntax: save(path, useBinary = false)_
_name: save_
_returns: void_
_returns_description: _
_parameters: string path, bool useBinary=false_
_access: public_
_version_started: 0071_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

 Saves the mesh at the passed path in the [PLY Format](http://en.wikipedia.org/wiki/PLY_(file_format)).

 There are two format options for PLY: a binary format and an ASCII format.
 By default, it will save using the ASCII format.
 Passing ``true`` into the ``useBinary`` parameter will save it in the binary format.

 If you're planning on reloading the mesh into ofMesh, ofMesh currently only supports loading the ASCII format.

 For more information, see the [PLY format specification](http://paulbourke.net/dataformats/ply/).





_description: _

Saves the mesh at the passed path in the [PLY Format](http://en.wikipedia.org/wiki/PLY_(file_format)).

There are two format options for PLY: a binary format and an ASCII format.
By default, it will save using the ASCII format.
Passing ``true`` into the ``useBinary`` parameter will save it in the binary format.

If you're planning on reloading the mesh into ofMesh, ofMesh currently only supports loading the ASCII format.

For more information, see the [PLY format specification](http://paulbourke.net/dataformats/ply/).





<!----------------------------------------------------------------------------->

###void setColor(index, &c)

<!--
_syntax: setColor(index, &c)_
_name: setColor_
_returns: void_
_returns_description: _
_parameters: ofIndexType index, const ofFloatColor &c_
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Set the color at the index in the colors vector.





_description: _

Set the color at the index in the colors vector.





<!----------------------------------------------------------------------------->

###void setColorForIndices(startIndex, endIndex, color)

<!--
_syntax: setColorForIndices(startIndex, endIndex, color)_
_name: setColorForIndices_
_returns: void_
_returns_description: _
_parameters: ofIndexType startIndex, ofIndexType endIndex, ofColor color_
_access: public_
_version_started: 0073_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###void setFromTriangles(&tris, bUseFaceNormal = false)

<!--
_syntax: setFromTriangles(&tris, bUseFaceNormal = false)_
_name: setFromTriangles_
_returns: void_
_returns_description: _
_parameters: const vector< ofMeshFace > &tris, bool bUseFaceNormal=false_
_access: public_
_version_started: 0073_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###void setIndex(index, val)

<!--
_syntax: setIndex(index, val)_
_name: setIndex_
_returns: void_
_returns_description: _
_parameters: ofIndexType index, ofIndexType val_
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

This sets the index at i.





_description: _

This sets the index at i.





<!----------------------------------------------------------------------------->

###void setMode(mode)

<!--
_syntax: setMode(mode)_
_name: setMode_
_returns: void_
_returns_description: _
_parameters: ofPrimitiveMode mode_
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Allows you to set the ofPrimitiveMode.
The available modes are OF_PRIMITIVE_TRIANGLES,
OF_PRIMITIVE_TRIANGLE_STRIP, OF_PRIMITIVE_TRIANGLE_FAN,
OF_PRIMITIVE_LINES, OF_PRIMITIVE_LINE_STRIP,
OF_PRIMITIVE_LINE_LOOP, OF_PRIMITIVE_POINTS





_description: _

Allows you to set the ofPrimitiveMode. The available modes are OF_PRIMITIVE_TRIANGLES, OF_PRIMITIVE_TRIANGLE_STRIP, OF_PRIMITIVE_TRIANGLE_FAN, OF_PRIMITIVE_LINES, OF_PRIMITIVE_LINE_STRIP, OF_PRIMITIVE_LINE_LOOP, OF_PRIMITIVE_POINTS





<!----------------------------------------------------------------------------->

###void setNormal(index, &n)

<!--
_syntax: setNormal(index, &n)_
_name: setNormal_
_returns: void_
_returns_description: _
_parameters: ofIndexType index, const ofVec3f &n_
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

\todo Documentation.





_description: _







<!----------------------------------------------------------------------------->

###void setTexCoord(index, &t)

<!--
_syntax: setTexCoord(index, &t)_
_name: setTexCoord_
_returns: void_
_returns_description: _
_parameters: ofIndexType index, const ofVec2f &t_
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###void setVertex(index, &v)

<!--
_syntax: setVertex(index, &v)_
_name: setVertex_
_returns: void_
_returns_description: _
_parameters: ofIndexType index, const ofVec3f &v_
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###void setupIndicesAuto()

<!--
_syntax: setupIndicesAuto()_
_name: setupIndicesAuto_
_returns: void_
_returns_description: _
_parameters: _
_access: public_
_version_started: _
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _

Allow you to set up the indices automatically when you add a vertex.





_description: _

Allow you to set up the indices automatically when you add a vertex.





<!----------------------------------------------------------------------------->

###void smoothNormals(angle)

<!--
_syntax: smoothNormals(angle)_
_name: smoothNormals_
_returns: void_
_returns_description: _
_parameters: float angle_
_access: public_
_version_started: 0073_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###ofMesh sphere(radius, res = 12, mode = OF_PRIMITIVE_TRIANGLE_STRIP)

<!--
_syntax: sphere(radius, res = 12, mode = OF_PRIMITIVE_TRIANGLE_STRIP)_
_name: sphere_
_returns: ofMesh_
_returns_description: _
_parameters: float radius, int res=12, ofPrimitiveMode mode=OF_PRIMITIVE_TRIANGLE_STRIP_
_access: public_
_version_started: 0073_
_version_deprecated: _
_summary: _
_constant: False_
_static: True_
_visible: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###bool usingColors()

<!--
_syntax: usingColors()_
_name: usingColors_
_returns: bool_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0071_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###bool usingIndices()

<!--
_syntax: usingIndices()_
_name: usingIndices_
_returns: bool_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0072_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###bool usingNormals()

<!--
_syntax: usingNormals()_
_name: usingNormals_
_returns: bool_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0071_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###bool usingTextures()

<!--
_syntax: usingTextures()_
_name: usingTextures_
_returns: bool_
_returns_description: _
_parameters: _
_access: public_
_version_started: 0071_
_version_deprecated: _
_summary: _
_constant: False_
_static: False_
_visible: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

##Variables



###bool bColorsChanged

<!--
_name: bColorsChanged_
_type: bool_
_access: private_
_version_started: 007_
_version_deprecated: _
_summary: _
_visible: True_
_constant: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###bool bFacesDirty

<!--
_name: bFacesDirty_
_type: bool_
_access: private_
_version_started: 0073_
_version_deprecated: _
_summary: _
_visible: True_
_constant: False_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###bool bIndicesChanged

<!--
_name: bIndicesChanged_
_type: bool_
_access: private_
_version_started: 007_
_version_deprecated: _
_summary: _
_visible: True_
_constant: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###bool bNormalsChanged

<!--
_name: bNormalsChanged_
_type: bool_
_access: private_
_version_started: 007_
_version_deprecated: _
_summary: _
_visible: True_
_constant: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###bool bTexCoordsChanged

<!--
_name: bTexCoordsChanged_
_type: bool_
_access: private_
_version_started: 007_
_version_deprecated: _
_summary: _
_visible: True_
_constant: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###bool bVertsChanged

<!--
_name: bVertsChanged_
_type: bool_
_access: private_
_version_started: 007_
_version_deprecated: _
_summary: _
_visible: True_
_constant: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###ofFloatColor colors

<!--
_name: colors_
_type: ofFloatColor_
_access: private_
_version_started: 007_
_version_deprecated: _
_summary: _
_visible: True_
_constant: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###ofMeshFace faces

<!--
_name: faces_
_type: ofMeshFace_
_access: private_
_version_started: 0073_
_version_deprecated: _
_summary: _
_visible: True_
_constant: False_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###ofIndexType indices

<!--
_name: indices_
_type: ofIndexType_
_access: private_
_version_started: 007_
_version_deprecated: _
_summary: _
_visible: True_
_constant: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###ofPrimitiveMode mode

<!--
_name: mode_
_type: ofPrimitiveMode_
_access: private_
_version_started: 007_
_version_deprecated: _
_summary: _
_visible: True_
_constant: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###ofVec3f normals

<!--
_name: normals_
_type: ofVec3f_
_access: private_
_version_started: 007_
_version_deprecated: _
_summary: _
_visible: True_
_constant: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###ofVec2f texCoords

<!--
_name: texCoords_
_type: ofVec2f_
_access: private_
_version_started: 007_
_version_deprecated: _
_summary: _
_visible: True_
_constant: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###bool useColors

<!--
_name: useColors_
_type: bool_
_access: private_
_version_started: 0071_
_version_deprecated: _
_summary: _
_visible: True_
_constant: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###bool useIndices

<!--
_name: useIndices_
_type: bool_
_access: private_
_version_started: 0072_
_version_deprecated: _
_summary: _
_visible: True_
_constant: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###bool useNormals

<!--
_name: useNormals_
_type: bool_
_access: private_
_version_started: 0071_
_version_deprecated: _
_summary: _
_visible: True_
_constant: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###bool useTextures

<!--
_name: useTextures_
_type: bool_
_access: private_
_version_started: 0071_
_version_deprecated: _
_summary: _
_visible: True_
_constant: True_
_advanced: False_
-->

_inlined_description: _







_description: _







<!----------------------------------------------------------------------------->

###ofVec3f vertices

<!--
_name: vertices_
_type: ofVec3f_
_access: private_
_version_started: 007_
_version_deprecated: _
_summary: _
_visible: True_
_constant: True_
_advanced: False_
-->

_inlined_description: _

\}





_description: _







<!----------------------------------------------------------------------------->

