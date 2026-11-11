
import bpy
import math
import os

# Scene reset
bpy.ops.object.select_all(action="SELECT")
bpy.ops.object.delete(use_global=False)

scene = bpy.context.scene
scene.render.engine = "BLENDER_EEVEE_NEXT"
scene.render.resolution_x = 480
scene.render.resolution_y = 854
scene.render.resolution_percentage = 100
scene.render.fps = 12
scene.frame_start = 1
scene.frame_end = 48

# Background
scene.world.color = (0.025, 0.025, 0.06)

# Floor
bpy.ops.mesh.primitive_plane_add(size=200, location=(0, 0, -1))
floor = bpy.context.object
floor.name = "Floor"
mat = bpy.data.materials.new("Midnight Blue")
mat.diffuse_color = (0.025, 0.08, 0.16, 1)
floor.data.materials.append(mat)

# Animated character: a bright bouncing sphere
bpy.ops.mesh.primitive_uv_sphere_add(
    segments=32, ring_count=16, location=(0, 0, 0)
)
ball = bpy.context.object
ball.name = "Character"
bpy.ops.object.shade_smooth()

mat = bpy.data.materials.new("Electric Orange")
mat.diffuse_color = (1.0, 0.18, 0.025, 1)
ball.data.materials.append(mat)

for frame, height in [(1, 0), (12, 2.3), (24, 0), (36, 1.5), (48, 0)]:
    ball.location.z = height
    ball.keyframe_insert(data_path="location", frame=frame)

# Camera
bpy.ops.object.camera_add(location=(7, -11, 5))
camera = bpy.context.object
camera.rotation_euler = (math.radians(68), 0, math.radians(33))
camera.data.lens = 45
scene.camera = camera

# Lighting
bpy.ops.object.light_add(type="AREA", location=(1, -4, 7))
light = bpy.context.object
light.data.energy = 1000
light.data.shape = "DISK"
light.data.size = 6

# Render settings
scene.render.image_settings.file_format = "PNG"
scene.render.filepath = "/tmp/frame_"
scene.render.resolution_percentage = 60
scene.render.resolution_x = 360
scene.render.resolution_y = 640

# Save the Blender project
bpy.ops.wm.save_as_mainfile(filepath="/tmp/prototype.blend")

# Render animation frames
bpy.ops.render.render(animation=True)
