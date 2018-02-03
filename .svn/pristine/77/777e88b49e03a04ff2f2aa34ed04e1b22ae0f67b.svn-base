# multiAgents.py
# --------------
# Licensing Information: Please do not distribute or publish solutions to this
# project. You are free to use and extend these projects for educational
# purposes. The Pacman AI projects were developed at UC Berkeley, primarily by
# John DeNero (denero@cs.berkeley.edu) and Dan Klein (klein@cs.berkeley.edu).
# For more info, see http://inst.eecs.berkeley.edu/~cs188/sp09/pacman.html

from util import manhattanDistance
import searchAgents
import search
from game import Directions
import random, util
import math

from game import Agent

class ReflexAgent(Agent):
  """
    A reflex agent chooses an action at each choice point by examining
    its alternatives via a state evaluation function.

    The code below is provided as a guide.  You are welcome to change
    it in any way you see fit, so long as you don't touch our method
    headers.
  """


  def getAction(self, gameState):
    """
    You do not need to change this method, but you're welcome to.

    getAction chooses among the best options according to the evaluation function.

    Just like in the previous project, getAction takes a GameState and returns
    some Directions.X for some X in the set {North, South, West, East, Stop}
    """
    # Collect legal moves and successor states
    legalMoves = gameState.getLegalActions()

    # Choose one of the best actions
    scores = [self.evaluationFunction(gameState, action) for action in legalMoves]
    bestScore = max(scores)
    bestIndices = [index for index in range(len(scores)) if scores[index] == bestScore]
    chosenIndex = random.choice(bestIndices) # Pick randomly among the best

    "Add more of your code here if you want to"
    #print " "

    return legalMoves[chosenIndex]

  def evaluationFunction(self, currentGameState, action):
    """
    Design a better evaluation function here.

    The evaluation function takes in the current and proposed successor
    GameStates (pacman.py) and returns a number, where higher numbers are better.

    The code below extracts some useful information from the state, like the
    remaining food (newFood) and Pacman position after moving (newPos).
    newScaredTimes holds the number of moves that each ghost will remain
    scared because of Pacman having eaten a power pellet.

    Print out these variables to see what you're getting, then combine them
    to create a masterful evaluation function.
    """
    # Useful information you can extract from a GameState (pacman.py)
    successorGameState = currentGameState.generatePacmanSuccessor(action)
    newPos = successorGameState.getPacmanPosition()
    newFood = successorGameState.getFood().asList()
    newGhostStates = successorGameState.getGhostStates()
    newScaredTimes = [ghostState.scaredTimer for ghostState in newGhostStates]
    "*** YOUR CODE HERE ***"
    currentFood = currentGameState.getFood().asList()

    ateFoodReward = 0

    if len(currentFood) > len(newFood):
        ateFoodReward = 100

    eatenByGhostReward = 0

    newGhostPosition = [ x.getPosition() for x in newGhostStates]
    newGhostPosTime = zip(newGhostPosition, newScaredTimes)

    if successorGameState.isLose():
        eatenByGhostReward = -50000

    newGhostDistances = [ manhattanDistance(newPos, pos) for (pos, time) in newGhostPosTime if time == 0]
    #totalDistance = sum(newGhostDistances)
    ghostDistanceReward = 0
    if len(newGhostDistances) > 0:
        ghostDistanceReward = -500*math.exp(min(newGhostDistances) * -1)

    ghostScaredTimes = [time for (pos, time) in newGhostPosTime if time > 0 ]
    if len(ghostScaredTimes) != 0:
        freedomTime = min(ghostScaredTimes)
    else:
        freedomTime = 0
    freedomReward = 20*freedomTime

    chaseGhostPosTime = [time - manhattanDistance(newPos, pos) for (pos, time) in newGhostPosTime if time > 0]
    chaseReward = 0
    if len(chaseGhostPosTime) > 0:
        chaseReward = 10 * max(chaseGhostPosTime)


    foodSearchProblem = searchAgents.AnyFoodSearchProblem(successorGameState)
    distanceToFood = search.bfs(foodSearchProblem)
    if distanceToFood == None:
        foodDistanceReward = 0
    else:
        foodDistanceReward = max(100 - (5*len(distanceToFood)), 0)


    #print "pos %s action %s ateFoodReward %i eatenByGhost %i ghostDistanceReward %i freedomReward %i chaseReward %i foodDistanceReward %i" %(currentGameState.getPacmanPosition(),action,ateFoodReward,eatenByGhostReward,ghostDistanceReward, freedomReward, chaseReward, foodDistanceReward)
    return ateFoodReward + eatenByGhostReward + ghostDistanceReward + foodDistanceReward + freedomReward + chaseReward



    ##return successorGameState.getScore()

def scoreEvaluationFunction(currentGameState):
  """
    This default evaluation function just returns the score of the state.
    The score is the same one displayed in the Pacman GUI.

    This evaluation function is meant for use with adversarial search agents
    (not reflex agents).
  """
  return currentGameState.getScore()

class MultiAgentSearchAgent(Agent):
  """
    This class provides some common elements to all of your
    multi-agent searchers.  Any methods defined here will be available
    to the MinimaxPacmanAgent, AlphaBetaPacmanAgent & ExpectimaxPacmanAgent.

    You *do not* need to make any changes here, but you can if you want to
    add functionality to all your adversarial search agents.  Please do not
    remove anything, however.

    Note: this is an abstract class: one that should not be instantiated.  It's
    only partially specified, and designed to be extended.  Agent (game.py)
    is another abstract class.
  """

  def __init__(self, evalFn = 'scoreEvaluationFunction', depth = '2'):
    self.index = 0 # Pacman is always agent index 0
    self.evaluationFunction = util.lookup(evalFn, globals())
    self.depth = int(depth)

class MinimaxAgent(MultiAgentSearchAgent):
  """
    Your minimax agent (question 2)
  """

  def getAction(self, gameState):
    """
      Returns the minimax action from the current gameState using self.depth
      and self.evaluationFunction.

      Here are some method calls that might be useful when implementing minimax.

      gameState.getLegalActions(agentIndex):
        Returns a list of legal actions for an agent
        agentIndex=0 means Pacman, ghosts are >= 1

      Directions.STOP:
        The stop direction, which is always legal

      gameState.generateSuccessor(agentIndex, action):
        Returns the successor game state after an agent takes an action

      gameState.getNumAgents():
        Returns the total number of agents in the game
    """
    "*** YOUR CODE HERE ***"
    #handle pacman
    numberOfAgents = gameState.getNumAgents()
    filterStop = lambda x: x != Directions.STOP
    maxDepth = self.depth
    def maxValue(index, depth, gameState):
        #print(" ")
        #print("max")
        if depth >= maxDepth:
            return self.evaluationFunction(gameState)
        currentScore = self.evaluationFunction(gameState)
        for action in filter(filterStop, gameState.getLegalActions(index)):
            nextGameState = gameState.generateSuccessor(index, action)
            nextIndex = (index +1) % numberOfAgents
            score = minValue(nextIndex, depth+1, nextGameState)
            currentScore = max(score, currentScore)
        return currentScore


    def minValue(index, depth, gameState):
        #print(" ")
        #print("min")

        if depth >= maxDepth:
            return self.evaluationFunction(gameState)
        #currentScore = float("inf")
        currentScore = self.evaluationFunction(gameState)
        for action in  gameState.getLegalActions(index):
            nextGameState = gameState.generateSuccessor(index, action)
            nextIndex = (index +1) % numberOfAgents
            if nextIndex == 0:
                score = maxValue(nextIndex, depth+1, nextGameState)
            else:
                score = minValue(nextIndex, depth+1, nextGameState)
            currentScore = min(score, currentScore)
        return currentScore

    bestScore = -float("inf")
    bestAction = Directions.STOP
    for action in filter(filterStop, gameState.getLegalActions(0)):
       nextGameState = gameState.generateSuccessor(0, action)
       score = minValue(1, 0, nextGameState)

       if score > bestScore:
            bestScore = score
            bestAction = action
    return bestAction

class AlphaBetaAgent(MultiAgentSearchAgent):
  """
    Your minimax agent with alpha-beta pruning (question 3)
  """

  def getAction(self, gameState):
    """
      Returns the minimax action using self.depth and self.evaluationFunction
    """
    "*** YOUR CODE HERE ***"
    numberOfAgents = gameState.getNumAgents()
    filterStop = lambda x: x != Directions.STOP
    maxDepth = self.depth

    def alphabeta(node, depth, alpha, beta, index):
        if depth == maxDepth or node.isWin() or node.isLose():
            return (self.evaluationFunction(node), None)
        # Check maximizing player
        if index % numberOfAgents == 0:
            value = -float("inf")
            bestAction = None
            for action in node.getLegalActions(index):
                nextGameState = node.generateSuccessor(index, action)
                nextIndex = (index + 1) % numberOfAgents
                (score, _) = alphabeta(nextGameState, depth+1, alpha, beta, nextIndex)
                if score > value:
                    value = score
                    bestAction = action
                if beta <= value:
                    break
                alpha = max(alpha, value)
            return (value, bestAction)
        else:
            value = float("inf")
            bestAction = None
            for action in node.getLegalActions(index):
                nextGameState = node.generateSuccessor(index, action)
                nextIndex = (index + 1) % numberOfAgents
                (score, _) = alphabeta(nextGameState, depth +1, alpha, beta, nextIndex)
                if score < value:
                    value = score
                    bestAction = action
                if beta <= value:
                    break
                beta = min(beta, value)
            return (value, bestAction)
    (score, bestAction) = alphabeta(gameState, 0, -float("inf"), +float("inf"), 0)
    print score
    return bestAction

class ExpectimaxAgent(MultiAgentSearchAgent):
  """
    Your expectimax agent (question 4)
  """

  def getAction(self, gameState):
    """
      Returns the expectimax action using self.depth and self.evaluationFunction

      All ghosts should be modeled as choosing uniformly at random from their
      legal moves.
    """
    "*** YOUR CODE HERE ***"


    numberOfAgents = gameState.getNumAgents()
    filterStop = lambda x: x != Directions.STOP
    maxDepth = self.depth

    def value(index, depth, gameState):
        if depth >= maxDepth:
            return (self.evaluationFunction(gameState))
        if index == 0:
            return maxValue(index, depth, gameState)
        else:
            return expValue(index,depth, gameState)

    def maxValue(index, depth, gameState):
        currentScore = -float("inf")
        actions = filter(filterStop, gameState.getLegalActions(index))
        for action in actions:
            nextGameState = gameState.generateSuccessor(index, action)
            nextIndex = (index + 1) % numberOfAgents
            score = value(nextIndex, depth+1, gameState)
            currentScore = max(score)
        return currentScore

    def expValue(index, depth, gameState):
        currentScore = 0
        actions = gameState.getLegalActions(index)
        for action in actions:
            nextGameState = gameState.generateSuccessor(index, action)
            nextIndex = (index + 1) % numberOfAgents
            p = 1/float(len(actions))
            score = value(nextIndex, depth+1, gameState)
            currentScore = currentScore + p * score
        return currentScore

    bestScore = -float("inf")
    bestAction = Directions.STOP
    for action in filter(filterStop, gameState.getLegalActions(0)):
       nextGameState = gameState.generateSuccessor(0, action)
       score = value(1, 1, nextGameState)
       if score > bestScore:
            bestScore = score
            bestAction = action
    return bestAction




def betterEvaluationFunction(currentGameState):
  """
    Your extreme ghost-hunting, pellet-nabbing, food-gobbling, unstoppable
    evaluation function (question 5).

    DESCRIPTION: <write something here so we know what you did>
  """
  "*** YOUR CODE HERE ***"


class ContestAgent(MultiAgentSearchAgent):
  """
    Your agent for the mini-contest
  """

  def getAction(self, gameState):
    """
      Returns an action.  You can use any method you want and search to any depth you want.
      Just remember that the mini-contest is timed, so you have to trade off speed and computation.

      Ghosts don't behave randomly anymore, but they aren't perfect either -- they'll usually
      just make a beeline straight towards Pacman (or away from him if they're scared!)
    """
    "*** YOUR CODE HERE ***"
    util.raiseNotDefined()
