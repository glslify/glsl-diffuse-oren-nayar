# glsl-diffuse-oren-nayar

The [Oren-Nayar](https://en.wikipedia.org/wiki/Oren%E2%80%93Nayar_reflectance_model) diffuse lighting model implemented in GLSL.

# Example

```glsl
#pragma glslify: orenNayar = require(glsl-diffuse-orenNayar)

uniform vec3 lightPosition, eyePosition;

varying vec3 surfacePosition, surfaceNormal;

void main() {
  //Light and view geometry
  vec3 lightDirection = normalize(lightPosition - surfacePosition);
  vec3 viewDirection = normalize(eyePosition - surfacePosition);

  //Surface properties
  vec3 normal = normalize(surfaceNormal);
  
  //Compute diffuse light intensity
  float power = orenNayar(
    lightDirection,
    viewDirection, 
    normal,
    0.3,
    0.7);

  gl_FragColor = vec4(power,power,power,1.0);
}
```

# Usage

Install with npm:

```
npm install glsl-diffuse-oren-nayar
```

Then use with [glslify](https://github.com/stackgl/glslify).

# API

```glsl
#pragma glslify: orenNayar = require(glsl-diffuse-oren-nayar)
```

##### `float orenNayar(vec3 lightDir, vec3 viewDir, vec3 normal, float roughness, float albedo)`
Computes the diffuse intensity in the Lambertian model

* `lightDir` is a *unit length* `vec3` pointing from the surface point toward the light
* `viewDir` is a *unit length* `vec3` pointing toward the camera
* `normal` is the *unit length* surface normal at the sample point
* `roughness` is a parameter between 0 and 1 measuring the surface roughness.  0 for smooth, 1 for matte
* `albedo` measures the intensity of the diffuse reflection.  Values `>0.96` do not conserve energy

**Returns** A `float` representing the diffuse light intensity

# License
(c) 2014 Mikola Lysenko. MIT License