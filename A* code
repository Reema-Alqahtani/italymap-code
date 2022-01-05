import heapq

# heap algorithm and its already exist in Python
class heapQueue: 
    def __init__(self): # its like a constructor in java, "__init__" came always with class
        self.queue = []

    def push(self, city, f_cost): # method to take to var and push them in queue array " self.queue = []"  
        heapq.heappush(self.queue, (f_cost, city) ) # and its look like this => queue=[(f_cost,city),...]

    def pop(self): # this method will remove and return the last index was pushed/headed 
        return heapq.heappop(self.queue)[1] # 0 is key , 1 is value, means city in array queue

    def isEmpty(self): # chick if the queue are empty or not 
        if self.queue: # if not empty return true
            return True
        else:
            return False # if empty return false 


class ctNode: # class contains two var city + distance from node_distance() method
    def __init__(self, city, distance):
        self.city = str(city)
        self.distance = int(distance) 


italy = {} # {key:value}

def node_dictionary(): # this method read the cites from italy.txt and rewrite all of the cites into "italy = {}"  
    file = open("italy.txt", 'r') #  anything from file is return as String
    for STR in file: # for each loop
        line = STR.split(',')
        c1 = line[0] # c1 = city1
        c2 = line[1] # c2 = city2
        d = int(line[2]) # d = distance
        italy.setdefault(c1, []).append(ctNode(c2, d)) # {'key' , ['c2','d']}
        italy.setdefault(c2, []).append(ctNode(c1, d)) 

italy_h = {} # {key:value}=> {node : hd }

def heuristic_dictionary(): # this method read the cites and there heuristic from italy_h.txt
    file = open("italy_h.txt", 'r') #  anything from file is return as String
    for STR in file: # for each loop
        line = STR.split(",")# STR type array
        node = line[0] # node = city
        hd = int(line[1]) # hd = heuristic distance
        italy_h[node] = hd # make node as key and the heuristic distance as a value 
    return italy_h


def heuristic(city_key , dict_h): # return heuristic value
    return dict_h[city_key]


def aStar(start_state, goal_state):# algorithm A*
    path = {}
    g_distance = {} 
    q = heapQueue() # q is object from class heapQueue 
    h = heuristic_dictionary()# h => dictionary of italy_h 

    q.push(start_state, 0) 
    g_distance[start_state] = 0
    path[start_state] = None
    

    
    while q.isEmpty(): # if empty will stop the loop 
        curr_node = q.pop() # remove+return the node from queue to curr_node

        if curr_node == goal_state:
            break 

        for child in italy[curr_node]: # child is value form key curr_node and value is obj from class ctNode
            g_cost = g_distance[curr_node] + int(child.distance)
            
            #  if child from parent curr_node not exist in g_distance then add the child to it
            #  or g_cost of parent smallest then the child cost then update the cost 
            if child.city not in g_distance or g_cost < g_distance[child.city]: 
                g_distance[child.city] = g_cost
                f_cost = g_cost + heuristic(child.city, h)
                q.push(child.city, f_cost) 
                path[child.city] = curr_node
                
    print_path(start_state, goal_state, path, g_distance) 


finalpath = []  
def final_path(goal_state, path): # to order the cites from goal to start
    if path.get(goal_state) is not None: # if the node have a parent  
        finalpath.append(goal_state)    
        final_path(path[goal_state] , path)   
        
        
def print_path(start_state, goal_state, path, g_distance): # to order the cites from start to goal
    final_path(goal_state , path)
    finalpath.append(start_state)
    finalpath.reverse()
    print("The train route in italy")
    print("Path :" + str(finalpath))
    print("cost : " + str(g_distance[goal_state]))


    
# like main method in java 

italyCity = ["Milan", "Taranto", "Bari","Reggio Calabria", "Naples", "Roma", "Ancona", 
             "Bologna", "Venice", "Verona","Bolzano Bozen","Turin","Genoa","Florence"]
start = input("Please enter the city you want to start from: ")
s = start.capitalize() # change all liters into capitalize
while s not in italyCity:
    print("SORRY", s ,"is incorrect or out of our range\n please choose from these cities:")
    print("'Milan' 'Taranto' 'Bari' 'Reggio Calabria' 'Naples' 'Roma' 'Ancona'")
    print("'Bologna' 'Venice' 'Verona' 'Bolzano Bozen' 'Turin' 'Genoa' 'Florence'")
    start = input("enter the city: ")
    s = start.capitalize() # change all liters into capitalize


goal = input("Please enter the city you want to go to: ")
g = goal.capitalize() # change all liters into capitalize
while g not in italyCity:
    print("SORRY", g ,"is incorrect or out of our range\n please choose from these cities:")
    print("'Milan' 'Taranto' 'Bari' 'Reggio Calabria' 'Naples' 'Roma' 'Ancona'")
    print("'Bologna' 'Venice' 'Verona' 'Bolzano Bozen' 'Turin' 'Genoa' 'Florence'")
    goal = input("enter the city: ")
    g = goal.capitalize() # change all liters into capitalize


node_dictionary()
aStar(s, g)


