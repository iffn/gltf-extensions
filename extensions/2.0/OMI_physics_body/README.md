# OMI_physics_body

## Contributors

- Aaron Franke, Godot Engine.
- Mauve Signweaver, Mauve Software Inc.

## Status

Open Metaverse Interoperability Group Stage 1 Proposal

## Dependencies

Written against the glTF 2.0 spec.

Depends on the `OMI_physics_shape` spec to be useful.

## Overview

This extension allows for specifying physics bodies in glTF scenes.

Nodes with the `OMI_physics_body` extension may define motion, collider, and trigger properties.

If a node with a collider shape does not have a motion property on itself or an ancestor node, it should be a static solid object that does not move.

### Example:

This example defines a physics node with dynamic motion and a single box collider:

```json
{
    "asset": {
        "version": "2.0"
    },
    "extensions": {
        "OMI_physics_shape": {
            "shapes": [
                {
                    "type": "box",
                    "box": {
                        "size": [1, 2, 3]
                    }
                }
            ]
        }
    },
    "extensionsUsed": [
        "OMI_physics_body",
        "OMI_physics_shape"
    ],
    "nodes": [
        {
            "extensions": {
                "OMI_physics_body": {
                    "motion": {
                        "type": "dynamic"
                    },
                    "collider": {
                        "shape": 0
                    }
                }
            },
            "name": "DynamicBox"
        }
    ],
    "scene": 0,
    "scenes": [{ "nodes": [0] }]
}
```

The above example shows dynamic motion and collision shape specified on one node. A nearly identical example using 2 nodes can be found in [examples/basic/dynamic_box.gltf](examples/basic/dynamic_box.gltf).

More example assets can be found in the [examples/](examples/) folder. All of these examples use both `OMI_physics_shape` and `OMI_physics_body`.

## glTF Schema Updates

This extension consists of a new `OMI_physics_body` data structure which can be added to a glTF node.

The extension must also be added to the glTF's `extensionsUsed` array and because it is optional, it does not need to be added to the `extensionsRequired` array.

The extension is intended to be used together with `OMI_physics_shape`, which defines the shapes used by the `"shape"` properties inside of the `"collider"` and `"trigger"` sub-JSON properties.

### Property Summary

|              | Type | Description                                                  | Default value |
| ------------ | ---- | ------------------------------------------------------------ | ------------- |
| **motion**   | JSON | If present, this node has its motion controlled by physics.  | `null`        |
| **collider** | JSON | If present, this node is solid and can be collided with.     | `null`        |
| **trigger**  | JSON | If present, this node is non-solid and can act as a trigger. | `null`        |

Each of these properties are recommended to be defined on separate nodes. This results in a very clear, simple, and portable document structure, and ensures that each behavior has its own transform. However, they may also be all defined on the same node. Implementations must support all of these cases in order to be compliant.

#### Motion

If a node has the `"motion"` property defined, its transform is driven by the physics engine.

The list of motion properties and their details can be found in the [README.motion.md](README.motion.md) file.

#### Collider

If a node has the `"collider"` property defined, it is a solid collider node that objects can collide with.

The list of collider properties and their details can be found in the [README.collider.md](README.collider.md) file. Nodes with a `"collider"` property may have a physics material, which is detailed in the [README.collider.md](README.collider.md) file. Nodes with a `"collider"` property may have a collision filter, which is detailed in a separate file, the [README.trigger.md](README.trigger.md) file.

#### Trigger

If a node has the `"trigger"` property defined, it is a non-solid trigger that can detect when objects enter it.

The list of trigger properties and their details can be found in the [README.trigger.md](README.trigger.md) file. Nodes with a `"trigger"` property may have a collision filter, which is detailed in the [README.trigger.md](README.trigger.md) file.

### JSON Schema

See [node.OMI_physics_body.schema.json](schema/node.OMI_physics_body.schema.json) for the main node schema, and these for the sub-JSON property schemas:
- Motion: [node.OMI_physics_body.motion.schema.json](schema/node.OMI_physics_body.motion.schema.json)
- Collider: [node.OMI_physics_body.collider.schema.json](schema/node.OMI_physics_body.collider.schema.json)
- Trigger: [node.OMI_physics_body.trigger.schema.json](schema/node.OMI_physics_body.trigger.schema.json)
- Document-level: [glTF.OMI_physics_body.schema.json](schema/glTF.OMI_physics_body.schema.json)
- Collision Filter: [glTF.OMI_physics_body.collision_filter.schema.json](schema/glTF.OMI_physics_body.collision_filter.schema.json)
- Physics Material: [glTF.OMI_physics_body.material.schema.json](schema/glTF.OMI_physics_body.material.schema.json)

## Known Implementations

- Godot Engine: https://github.com/godotengine/godot/pull/78967

## Resources:

- Unity Colliders: https://docs.unity3d.com/Manual/CollidersOverview.html
- Unity PhysicMaterial: https://docs.unity3d.com/Manual/class-PhysicMaterial.html
- Unity Physics Layers: https://docs.unity3d.com/Manual/LayerBasedCollision.html
- Unreal Engine Physics Collision: https://dev.epicgames.com/documentation/en-us/unreal-engine/collision-in-unreal-engine
- Unreal Engine Physical Materials: https://dev.epicgames.com/documentation/en-us/unreal-engine/physical-materials-reference-for-unreal-engine
- Unreal Engine Collision Filtering: https://www.unrealengine.com/en-US/blog/collision-filtering
- Godot PhysicsBody3D: https://docs.godotengine.org/en/stable/classes/class_physicsbody3d.html
- Godot Area3D: https://docs.godotengine.org/en/stable/classes/class_area3d.html
- Godot RigidBody3D: https://docs.godotengine.org/en/stable/classes/class_rigidbody3d.html
- Wikipedia Moment of Inertia: https://en.wikipedia.org/wiki/Moment_of_inertia
- Wikipedia Rigid Body Dynamics: https://en.wikipedia.org/wiki/Rigid_body_dynamics
