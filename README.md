# glsl-diffuse-lambert

A simple Lambertian diffuse lighting model (somewhat trivial, but included for completeness).

# Example

```glsl
#pragma glslify: lambert = require(glsl-diffuse-lambert)

uniform vec3 lightPosition;

varying vec3 surfacePosition, surfaceNormal;

void main() {
  //Light geometry
  vec3 lightDirection = normalize(lightPosition - surfacePosition);

  //Surface properties
  vec3 normal = normalize(surfaceNormal);
  
  //Compute diffuse light intensity
  float power = lambert(
    lightDirection, 
    normal);

  gl_FragColor = vec4(power,power,power,1.0);
}
```

# Usage

Install with npm:

```
npm install glsl-diffuse-lambert
```

Then use with [glslify](https://github.com/stackgl/glslify).

# API

```glsl
#pragma glslify: lambert = require(glsl-diffuse-lambert)
```

##### `float lambert(vec3 lightDir, vec3 normal)`
Computes the diffuse intensity in the Lambertian model

* `lightDir` is a *unit length* `vec3` pointing from the surface point toward the light
* `normal` is the *unit length* surface normal at the sample point

**Returns** A `float` representing the diffuse light intensity

# License
(c) 2014 Mikola Lysenko. MIT License