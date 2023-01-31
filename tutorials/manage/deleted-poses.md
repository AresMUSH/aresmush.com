---
title: Restoring Deleted Scene Poses
description: 
layout: page
---

Although there is no UI to see it, the game does save deleted scene poses until the scene is shared. Once the scene is shared, deleted poses are gone forever.

You can access deleted poses with a coder character using the scene number. For example, for scene 27:

`ruby Scene[27].scene_poses.select { |s| s.is_deleted }`

This will give you a list of the deleted poses:

```
[#<AresMUSH::ScenePose:0x0000000111aee018 @attributes={:created_at=>"2023-01-08 02:49:51 -0500", :updated_at=>"2023-01-08 12:39:03 -0500", :character_id=>"9", :scene_id=>"1046", :pose=>"Test", :is_deleted=>"true", :history=>"[]"}, @_memo={}, @id="4595">]
```

You can restore a deleted pose using its ID. For example, the above pose had `@id="4595"`:

`ruby ScenePose[4595].update(is_deleted: false)`