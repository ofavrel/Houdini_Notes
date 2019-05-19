# Tileable Droplet Texture Tool 
## _Un outil permettant de créer des textures tileable de Droplets (Alpha, Normals) afin d'être utilisé dans un moteur de jeu (UE4/Unity/Godot)._


<br>

## Topics

### Droplet Meshes
* [Creation des meshes de Droplet](#Creation-des-meshes-de-Droplet)
* [Tileable Points](#tileable-points)
* [Fix Overlapping Droplet](#fix-overlapping-droplet)


### Creation des meshes de Droplet:

**Base**:\
    <ul>-
    _Half-Sphere\
    -Noise\
    -Variation_
    </ul>\
**Size**:\
    <ul>-
    _1 unit Sphere Size\
    -Center\
    -Orient Z_
    </ul>
**Depth Map**:\
    <ul>-
    _Bounding Box based Depth_\
    </ul>
### Tileable Points:
 
**Base**:\
    <ul>-_Scatter Pts on Txt Grid Size\
    -Randomize  Red Colors (to be used in later in Shader)\
    -Create a Copy Attribute\
    -Create N and Randomize_
    </ul>
**Tile it**:\
    <ul>-_Duplicate it 9 time on a grid Fashion\
    -Delete the Points Outside The Txt Grid Size with a Small Margin_\
    </ul>
**References**:\
    <ul>-https://richardlord.tumblr.com/page/2
    <br>
    -https://www.sidefx.com/tutorials/game-tools-mesh-tiler/
    </ul>

### Fix Overlapping Droplet:
 
**Base**:\
    <ul>-_Get the Nearest point of Each Points\
    -Create a Line and Calculate the Distance\
    -Promote the distance Attribute to the Point (Min)<br>
    -Divide it by two and use it as Pscale_
    </ul>
**References**:\
    <ul>-http://probiner.xyz/2018/07/09/houdini-non-intersecting-spheres-pscale-fitting/
    <br>
    -https://richardlord.tumblr.com/page/2
    <br>
    -https://forums.odforce.net/topic/19771-tesselating-spheres/
    <br>
    -https://www.sidefx.com/forum/topic/34136/
    <br>
    -https://vimeo.com/210226436
    <br>
    -Detangle Sop
    </ul>

### Copy Random Droplets on Tileable Target Points:
 
**Base**:\
    <ul>-_For-Each Pts Copy Random Variation\
    -Spare inputs references\
    -Compiled Blocks
    -Divide it by two and use it as Pscale_
    </ul>
**References**:\
    <ul>-https://www.sidefx.com/docs/houdini/copy/copytopoints.html#foreach
    <br>
    -https://www.toadstorm.com/blog/?p=493
    <br>
    -https://vimeo.com/222881605
    <br>
    -https://vimeo.com/213127548
    </ul>
