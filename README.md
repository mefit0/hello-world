# hello-world
project in LOCEN (Granato, Maglione, Lord etc)
Project notes/description:

#####################################################TEST

NOTES ON THE COMPUTATIONAL MODEL

- At the beginning they will work together, then:
-- Ilaria will specialise on AI and GOAL-Robots
-- Giovanni and William will work on 1 or 2 meccanisms of consciousness taken from the 4 of our theory: abstraction, specification, segmentation, chunking
- The task will be the one of the kitchen scenario (GOAL4) of GOAL-Robots. Advantages:
-- Synergies with the project GOAL-Robots
-- Very nice set up to test some preliminary ideas on consciousness elaborated with Giovanni, and related to goal-directed behaviour, flexible problem solving, etc.
-- Handy way to create many problem solving situations where consciousness mechanisms are very useful to flexibly solve the problems
- They will start with a simplified simulation:
-- Python + graphic library MatPlotLib (in the future PyQtGraph, much more fast but also much more difficult to use)
-- Simulation in 2D of objects: circle, square, triangle; in RGB; with varying size
- Hand is a dot. Action is  (x_0, y_0, x_1, y_1) indicating where hand does the `pick-up and place'
- As a consequence of action, object picked up at (x_0,y_0) will be placed at (x_1,y_1) without changing orientation

- Components of the system architecture:
-- A parameterised skill implementing the mapping:
      Input: condition=current_object_position=(x_0,y_0)
                 goal=desired_object_position_in_overall_goal_image=(x_1,y_1)
      Output: (x_0,y_0,x_1,y_1) action moving the hand
-- A goal-classifier:
      Input: looked object in overall-goal image
      Output: YES/NO, meaning it is a goal the system knows how to achieve or not
-- A goal-achievable-classifier:
      Input: looked object in overall-goal image +  looked object in current environment image
      Output: YES/NO, meaning it is an achievable goal from the current condition
-- Critical point of the functioning of the system (critical for scientific issues). The two classifiers are each formed by two components, stacked one on top of the other:
--- First component: Restricted Boltzmann Machine (RBM; 1 or more layers), learning in an unsupervised fashion to represent objects. Input: retina image. Output: hidden causes of image.
--- Second component: Input: hidden causes from RBM. Output: YES/NO.
--- The use of  a RBM is critical as will allow the system to disangangle situations, e.g. if the system sees a circle and a square over it, it might imagine a circle or a square (pattern completion). NOTE: this is one first possible `scientific catch' of the whole work: which others can we have?
-- Two attentional components (guided for now by bottom-up attention mechanisms based on image-constrasts):
--- The first one scans the memorised internal image of the overall-goal
--- The second one scans the current state of the world

- The scenario is the one of GOAL4 demonstrator, where:
-- Intrinsic phase:
- We will for now assume a hardwired system that has already learned the parameterised skill (through intrinsec motivations, goals, ect.)
- Extrinsic phase:
-- The system memorises the `overall-goal' state of the environment to be reached
-- The system is set in front of the current state of the environemnt after objects have been moved, and possibly also overlapped (in the intrinsic phase, we will start with 1 object and then complicate the situation with 2 non-overlapped, then 2 overlapped, then 3 with 1 never seen before, etc.)
-- Critical point on the functioning of the system (critical for the solution of the task by the system):
--- For each scanned point of the overall-goal-image, the goal-classifier tells if the seen image is a goal:
---- if NO: the system continues to scan the overall-goal-image without doing anything
---- if YES: the goal-achievable-classifier tells if the goal is achievable from the current state:
----- if NO: the system starts to scan the internal overall-goal image again
----- if YES: the system passes (x_0,y_0)=position_of_goal_in_overall-goal and (x_1,y_1)=position_of_object_in_current_environment_state to the parameterised skill for policy (action) generation and execution
