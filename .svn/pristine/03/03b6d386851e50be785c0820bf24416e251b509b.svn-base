# search.py
# ---------
# Licensing Information: Please do not distribute or publish solutions to this
# project. You are free to use and extend these projects for educational
# purposes. The Pacman AI projects were developed at UC Berkeley, primarily by
# John DeNero (denero@cs.berkeley.edu) and Dan Klein (klein@cs.berkeley.edu).
# For more info, see http://inst.eecs.berkeley.edu/~cs188/sp09/pacman.html

"""
In search.py, you will implement generic search algorithms which are called
by Pacman agents (in searchAgents.py).
"""

import util
from game import Directions

class SearchProblem:
    """
    This class outlines the structure of a search problem, but doesn't implement
    any of the methods (in object-oriented terminology: an abstract class).
    You do not need to change anything in this class, ever.
    """

    def getStartState(self):
        """
        Returns the start state for the search problem
        """
        util.raiseNotDefined()

    def isGoalState(self, state):
        """
          state: Search state
        Returns True if and only if the state is a valid goal state
        """
        util.raiseNotDefined()

    def getSuccessors(self, state):
        """
          state: Search state
        For a given state, this should return a list of triples,
        (successor, action, stepCost), where 'successor' is a
        successor to the current state, 'action' is the action
        required to get there, and 'stepCost' is the incremental
        cost of expanding to that successor
        """
        util.raiseNotDefined()

    def getCostOfActions(self, actions):
        """
         actions: A list of actions to take
        This method returns the total cost of a particular sequence of actions.  The sequence must
        be composed of legal moves
        """
        util.raiseNotDefined()


def tinyMazeSearch(problem):
    """
    Returns a sequence of moves that solves tinyMaze.  For any other
    maze, the sequence of moves will be incorrect, so only use this for tinyMaze
    """
    from game import Directions
    s = Directions.SOUTH
    w = Directions.WEST
    return  [s,s,w,s,w,w,s,w]

def depthFirstSearch(problem):
    """
    Search the deepest nodes in the search tree first
    [2nd Edition: p 75, 3rd Edition: p 87]
    Your search algorithm needs to return a list of actions that reaches
    the goal.  Make sure to implement a graph search algorithm
    [2nd Edition: Fig. 3.18, 3rd Edition: Fig 3.7].
    To get started, you might want to try some of these simple commands to
    understand the search problem that is being passed in:
    print "Start:", problem.getStartState()
    print "Is the start a goal?", problem.isGoalState(problem.getStartState())
    print "Start's successors:", problem.getSuccessors(problem.getStartState())
    """
    "*** YOUR CODE HERE ***"
    isVisited = {}
    path = {}

    startState = problem.getStartState()
    if problem.isGoalState(startState):
        return makePath(path, startState, startState)
    stateStack = util.Stack()
    stateStack.push((startState, None, 1, startState))
    while not stateStack.isEmpty():
        currentState, action, cost, previousState = stateStack.pop()
        path[currentState] = (previousState, action, cost)
        if problem.isGoalState(currentState):
            return makePath(path, startState, currentState)
        isVisited[currentState] = True

        for (s, a, c) in problem.getSuccessors(currentState):
            if isVisited.has_key(s):
                continue
            stateStack.push((s, a, c, currentState))



        
             
def makePath(path, startState, goalState):
    """
    makePath takes a dictionary in the form of an adjacency list in which
    the value associated with the key is the state, action, and cost to get
    to that key.
    """
    toReturn = []
    if startState == goalState:
        return toReturn

    currentState = goalState
    while True:
        previousState, action, cost = path[currentState]
        toReturn.append(action)
        if previousState == startState:
            toReturn.reverse()
            return toReturn
        currentState = previousState



def breadthFirstSearch(problem):
    """
    Search the shallowest nodes in the search tree first.
    [2nd Edition: p 73, 3rd Edition: p 82]
    """
    "*** YOUR CODE HERE ***"
    isVisited = {}
    inFringe = {}
    path = {}

    startState = problem.getStartState()
    stateQueue = util.Queue()
    stateQueue.push((startState, None, 1, startState))
    inFringe[startState] = True

    while not stateQueue.isEmpty():
        
        currentState, action, cost, previousState = stateQueue.pop()
        inFringe.pop(currentState,None)
        path[currentState] = (previousState, action, cost)
        isVisited[currentState] = True
        if problem.isGoalState(currentState):
            return makePath(path, startState, currentState)
        
        for (s, a, c) in problem.getSuccessors(currentState):

            if isVisited.has_key(s) or inFringe.has_key(s):
                continue
            stateQueue.push((s, a, c, currentState))
            inFringe[s] = True



def uniformCostSearch(problem):
    "Search the node of least total cost first. "
    "*** YOUR CODE HERE ***"
    isVisited = {}
    inFringe = {}
    distances = {}
    path = {}

    startState = problem.getStartState()

    if problem.isGoalState(startState):
        return makePath(path, startState, startState)

    
    stateStack = util.PriorityQueue()
    stateStack.push((startState, None, 1, startState), 0)
    inFringe[startState] = True

    distances[startState] = 0
    while not stateStack.isEmpty():
        currentState, action, cost, previousState = stateStack.pop()
        inFringe.pop(currentState,None)
        path[currentState] = (previousState, action, cost)
        if problem.isGoalState(currentState):
            return makePath(path, startState, currentState)
        isVisited[currentState] = True

        for (s, a, c) in problem.getSuccessors(currentState):
            distance = distances.get(s, float("inf"))
            alt = distances[currentState] + c
            if (isVisited.has_key(s) or inFringe.has_key(s)) and alt > distance:
                continue
            if alt <= distance:
                distances[s] = alt
                distance = alt
            stateStack.push((s, a, c, currentState), distance)
            inFringe[s] = True

def nullHeuristic(state, problem=None):
    """
    A heuristic function estimates the cost from the current state to the nearest
    goal in the provided SearchProblem.  This heuristic is trivial.
    """
    return 0

def aStarSearch(problem, heuristic=nullHeuristic):
    "Search the node of least total cost first. "
    "*** YOUR CODE HERE ***"
    isVisited = {}
    inFringe = {}
    fScore = {}
    gScore = {}
    path = {}

    startState = problem.getStartState()

    if problem.isGoalState(startState):
        return makePath(path, startState, startState)
    
    stateStack = util.PriorityQueue()
    stateStack.push((startState, None, 0, startState), 0)

    inFringe[startState] = True

    fScore[startState] = 0
    gScore[startState] = 0
    while not stateStack.isEmpty():
        currentState, action, cost, previousState = stateStack.pop()
        inFringe.pop(currentState,None)

        path[currentState] = (previousState, action, cost)
        if problem.isGoalState(currentState):
            return makePath(path, startState, currentState)
        isVisited[currentState] = True

        for (s, a, c) in problem.getSuccessors(currentState):
            g = gScore.get(s, float("inf"))
            tent_g = gScore[currentState] + c
            if isVisited.has_key(s):
                continue
            if not inFringe.has_key(s):
                inFringe[s] = True
            elif tent_g >= g:
                continue

            gScore[s] = tent_g
            fScore[s] = gScore[s] + heuristic(s, problem)
            stateStack.push((s, a, c, currentState), fScore[s])
        
    return []



# Abbreviations
bfs = breadthFirstSearch
dfs = depthFirstSearch
astar = aStarSearch
ucs = uniformCostSearch