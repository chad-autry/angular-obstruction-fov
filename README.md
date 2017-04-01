# angular-obstruction-fov
An algorithm for calculating FOV on co-ordinates relative to a viewer with angular FOV masks for each visible cell

# Features
* Only walks visible cells of a map, does not walk obstructed cells
* Computes angular masks for partial cell visibility
* Portals!
* Operates using co-ordinates relative to the viewer (needed for client/server security)
* Can handle visibility attenuation (fog)
* A limited set of Obstruction 'types' can allow for pre-calculation of obstruction angles
* Asymetric vision (can be made symetric I think)

# Algorithm
```psuedo-code
initialize a queue with the visible adjacent cells in the von Neumann neighborhood of the starting cell
//order in and out doesn't matter
the cells should be decorated with the relative co-ordinate to the viewer
the cells should be decorated with the incoming visibillity range they obstruct 
// the four cardinal squares each subtend an angle of pi/2, unless occupied cell blocks vision

while queue not empty
    pull cell from queue
    
```
