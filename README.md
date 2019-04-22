## Welcome to some Heuristic implemenations page __Intended for fun



### Contents
1. Dijkstra's algorithm
2. Prims Algorithm


```markdown
# Dijkstra's algorithm
import numpy as np
import sys
import matplotlib.pyplot as plt



def algo (graph, first = 0, length = 5, final_node = 4):
    

    spSet = [] #only selected nodes are added to this
    len_track = [1000]*length #keeping track of all the lengths known
    
   
    check = [False]*length #currently there are none added
    len_selected = [] # length of the selected path
    
    ###initializing the first node
    spSet.append(first) #adding the first node
    check[first] = True #changing the status to true
    len_track[first] = 0
    min_index = first
    
    
    while(check[final_node]  == False): # outer loop for checking termination
         
        last_node = spSet[-1]
  
        for j in range(0,length):

            if graph[last_node][j] != 0 and check[j] == False:

                if graph[last_node][j]+len_track[last_node] < len_track[j]:
                    index_selected = j
                    min_val = graph[last_node][j]+len_track[last_node]
                    len_track[index_selected] = min_val
        
        
        old = min_index
        min_value = sys.maxsize
        
        for i in range(0,len (len_track)): #finding the minimum in the array
            if check[i] == False:
                if min_value > len_track[i]:
                    min_value = len_track[i]
                    min_index = i

        
        
        spSet.append(min_index)     
        check[min_index] = True
        print ("The path is "+str(old)+" ---> "+ str(min_index) + " for a length of "+str(min_value))
        
    print ('Optimal path found after '+str(len(spSet))+' node evaluations!! Congrats :)')


    return spSet, len_selected
 

graph = [[0,2,0,6,0,4,0,5,10,0],[8,88,9,9,0,8,0,8,1,2,0],[3,8,5,5,0,6,7,3,4,5],[6,7,8,0,66,7,44,0,3,0],
         [0,5,66,7,8,9,0,4,0,4,56],[7,7,2,4,5,64,0,5,6,7],[0,0,0,5,4,3,2,0,3,4],[8,0,0,9,0,0,5,7,9,0],[3,4,5,6,0,0,0,5,0,3],
        [1,2,3,4,0,0,4,3,2,1]]


spSet, len_selected= algo(graph, 0,10,3)


#############################################################

print ('\n \n')
print ('Using a graph of any given size:: Please enter the size (enter whole number)')
a_input = int (input())
random_graph = np.random.rand(a_input,a_input)*77
spSet, len_selected= algo(random_graph, 0,a_input,a_input-1)




```




```markdown
# Prim's algorithm 

import numpy as np
import sys
import matplotlib.pyplot as plt



def algo (graph, first = 0, length = 5, final_node = 8):
    
    ## only the selected candidates will be added to this
    spSet = []
    check = [False]*length #currently there are none added
    len_selected = [] # length of the selected path
    
    ###initializing the first node
    spSet.append(first) #adding the first node
    check[first] = True #changing the status to true
    
    print ("The path taken by the algorithm was")
    
    while(check[final_node]  == False): # outer loop for checking termination
        
        
        track, spSet, check, min_val = search_iter(graph, spSet, length, check)
        old = spSet[-1]
        spSet.append(track)  # selecting only the best one amoung all the nodes checked. The selected node is added to the explored nodes list
        check[track] = True # updating the boolean vairable so that it is not explored again   
        len_selected.append(min_val)
        print ("The path is "+str(old)+" ---> "+ str(track) + " for a length of "+str(min_val))

    
    print ('Optimal path found after '+str(len(spSet))+' node evaluations!! Congrats :)')

    return spSet, len_selected
 



def search_iter(graph, spSet, length, check): # for each search iteration
          
    min_val = sys.maxsize # keeps track of the minimum value selected
    track = [] # keeps track of the node number selected

    for i in spSet: 
        for j in range(0,length):
            if graph[i][j] != 0 and check[j] == False:
                if graph[i][j] < min_val:
                    min_val = graph[i][j]
                    track = j
    
    return track, spSet, check, min_val

    


#graph = [[0,2,0,6,0],[2,0,3,8,5],[0,3,0,0,7],[6,8,0,0,9],[0,5,7,9,0]]


graph = [[0,2,0,6,0,4,0,5,10,0],[8,88,9,9,0,8,0,8,1,2,0],[3,8,5,5,0,6,7,3,4,5],[6,7,8,0,66,7,44,0,3,0],
         [0,5,66,7,8,9,0,4,0,4,56],[7,7,2,4,5,64,0,5,6,7],[0,0,0,5,4,3,2,0,3,4],[8,0,0,9,0,0,5,7,9,0],[3,4,5,6,0,0,0,5,0,3]]





spSet, len_selected= algo(graph, 0,10,9)

#############################################################

print ('\n \n')
print ('Using a graph of any given size:: Please enter the size (enter whole number)')
a_input = int (input())
random_graph = np.random.rand(a_input,a_input)*77
spSet, len_selected= algo(random_graph, 0,a_input,a_input-1)


