# glassimp

This is a small library of OpenGL utilities for use with the [Open Asset
Import Library](http://assimp.sourceforge.net/).

## Building

glassimp requires that assimp itself be installed, and locatable with
the pkg-config utility.

```
./configure PKG_CONFIG_PATH=/path/to/assimp/pkgconfig
make
make install
```

## Using

Currently, the main purpose of the library is to load triangulated
aiMesh objects into OpenGL vertex buffer objects. Given a mesh with
vertices, normals, and texture coordinates, a vertex buffer could be
filled this way:

```
aiMesh * mesh;

const GLuint nTriangles = glassimpTrianglesCount(mesh);
GLenum attribs[] = {
	GLASSIMP_VERTEX_ARRAY, GLASSIMP_NORMAL_ARRAY, GLASSIMP_TEXTURE_COORD_ARRAY
};
GLuint indices[] = {
	0, 0, 0
};
GLint sizes[] = {
	3, 3, 2
};
GLenum types[] = {
	GL_FLOAT, GL_FLOAT, GL_FLOAT
};
GLint sizes_out[3];
GLsizei strides_out[3];
GLvoid * pointers_out[3];
GLuint stride = glassimpTrianglesFormat(mesh,GL_TRUE,3,attribs,indices,sizes,types,0,sizes_out,strides_out,pointers_out);

GLuint vbo = 0;
glGenBuffers(1,&vbo);
glBindBuffer(GL_ARRAY_BUFFER,vbo);
glBufferData(GL_ARRAY_BUFFER,stride * nTriangles * 3,0,GL_STATIC_DRAW);
void * pvbo = glMapBuffer(GL_ARRAY_BUFFER,GL_WRITE_ONLY);
glassimpTrianglesLoadArrays(mesh,GL_TRUE,3,attribs,indices,sizes,types,pvbo);
glUnmapBuffer(GL_ARRAY_BUFFER);
```

A suitable vertex array object can be made as well:

```
GLuint vao = 0;
glGenVertexArrays(1,&vao);
glBindVertexArray(vao);
glassimpTrianglesSetPointers(mesh,locations,GL_TRUE,3,attribs,indices,sizes,types,0);
```
