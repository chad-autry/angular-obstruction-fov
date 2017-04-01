# angular-obstruction-fov
An algorithm for calculating FOV on co-ordinates relative to a viewer with angular FOV masks for each visible cell

# Features
* Does not walk obstructed cells (of course nothing might be visible depending on light/game logic)
* Computes angular masks for partial cell visibility
* Portals! (ignore comments on portals if complexity not desired)
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
if the cell is visible through a portal, it should be deorated with the transformation (translation + rotation)
the cell may be decorated with attenuation information (fog)
// the four cardinal squares each subtend an angle of pi/2, unless occupied cell blocks vision

while queue not empty
    pull cell from queue
    add visibility info to result with relative co-ords
        //What is visible depends on game logic
        //Visibillity should include the angles of the cell visible, can be omitted if full cell visible
        //Merge with any existing info for different visible angles
    if cell is furthest distance visible
        break
    calculate/lookup angles of any obstruction within the cell
    //If the types obstructions are static, the obstructed angles can be pre-computed for each relative co-ord
    //Could be fully obstructed, obstructed across any edge, obstructed across the middle (horizontal, middle, both diagonals)
    //Could be  obstructed in the middle
    
    if an obstruction is a portal (a portal should generally be one of the sides, and are one way
        add the cell on the other side of the portal to the queue (decorated same as initial cells)
        
    lookup the cells in the von Neuman neighborhood which are visible at the un-obstructed angles through the cell
    add them to the queue (decorated same as initial cells)
```
# Notes
* Cells are visited multiple times with distinct angles. It should be possible to merge them before processing
* The view is asymetric, but could be made symetric with some work
* Notice that diagonals from the viewer cannot be seen into if the shared von Neuman neighbors are obstructed
