# OMI_physics_body Joint Property

If a node has the `"joint"` property defined, it is a physics joint that constrains the relative motion of two bodies. The joint properties and the connected node must be defined.

## Joint Properties

|                     | Type      | Description                                                  | Default value        |
| ------------------- | --------- | ------------------------------------------------------------ | -------------------- |
| **joint**           | `integer` | The index of the joint in the top level physicsJoints array. | Required, no default |
| **connectedNode**   | `integer` | The index of the node to which this is connected.            | Required, no default |
| **enableCollision** | `boolean` | If true, allow the connected objects to collide.             | false                |

### Joint

The `"joint"` property is an integer index that references a joint in the document-level physicsJoints array in the `OMI_physics_body` extension. This property is required and has no default value.

The document-level joint object holds parameters that define the behavior of the joint, including constraints, limits, and drives/motors.

### Connected Node

The `"connectedNode"` property is an integer index that references another glTF node in the scene. This property is required and has no default value.

### Enable Collision

The `"enableCollision"` property is a boolean value. If true, allow the connected objects to collide. Connected objects do not collide with each other by default.

## JSON Schema

See [schema/node.OMI_physics_body.collider.schema.json](schema/node.OMI_physics_body.collider.schema.json) for the collider properties JSON schema.

## Joint Parameters

### Joint Limits

Joint limits, also known as joint constraints, allow restricting the relative motion of two glTF nodes connected by a joint. Limits can be set on the joint's position, rotation, or both.

### Joint Drives

Joint drives, also known as motors, allow applying forces to the connected nodes to drive them to a desired relative velocity. Drives can be set on the joint's linear velocity, angular velocity, or both.
