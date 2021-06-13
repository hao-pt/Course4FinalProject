# Course4FinalProject

In this project we will be implementing many of the behavioral and local
planning concepts discussed in Course 4. The goal of this project will
be to have a functional motion planning stack that can avoid both static
and dynamic obstacles while tracking the center line of a lane, while
also handling stop signs. To accomplish this, you will have to implement
behavioral planning logic, as well as static collision checking, path
selection, and velocity profile generation.

To do this assignment, the CARLA simulator along with the assignment
code needs to be installed. Please follow these instructions:

Install the CARLA simulator
===========================

Follow the CARLA Installation guide from a previous reading to install
the CARLA simulator.

Download the final project file
===============================

Download the following "Course4FinalProject.zip" file and unpack into
the subfolder folder "PythonClient" inside the "CarlaSimulator" (root)
folder. This will create a subfolder "Course4FinalProject" under
"PythonClient" which contains the assignment files.

[Course4FinalProject.zip](https://d3c33hcgiwev3.cloudfront.net/vI0lpI0fEem-xg4p7cmXwA_e77ed940c64e410dbb04a66a123836d7_Course4FinalProject.zip?Expires=1623715200&Signature=Qxq0XtcmGpdq8TzxNK7xCknJoHBTtALuHbW2tAYkkSfLLSPUeNJPGPZ9Tht3yXuATX9q6hiSmBmy8YUawoTHOm4xq7Tw7GlzhYuup3tNkxu5-GWzVCXkLTnAJjkWPsXpBPdhSjLjc3eTVNN-b-JvoRznpdvLXwosac2Tm2yxyJM_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A)

It is very important to have the contents of "Course4FinalProject.zip"
be under the folder "**PythonClient\\Course4FinalProject**" (for
Windows) or "**PythonClient/Course4FinalProject**" (for Ubuntu).
Installing it into another directory might cause runtime issues.

After successfully downloading CARLA and the assessment script, you can
now begin the assignment.

Implementing the Motion Planner
===============================

In this project, you will be editing the "**behavioural\_planner.py**",
"**collision\_checker.py**", "**local\_planner.py**",
"**path\_optimizer.py**", and "**velocity\_planner.py**" class files
(found inside the "**PythonClient\\Course4FinalProject**" (for Windows)
or "**PythonClient/Course4FinalProject**" (for Ubuntu) folder). This is
where you will implement your motion planner. There are 5 main aspects
of the planner you will need to implement, behaviour planning logic,
path generation, static collision checking, path selection, and velocity
profile generation. Let's go over each of these in kind.

Behaviour Planning Logic
------------------------

In this part of the project, you will implement the behavioural logic
required to handle a stop sign. As in the lecture videos, you will be
implementing a state machine that transitions between lane following,
deceleration to the stop sign, staying stopped, and back to lane
following, when it encounters a stop sign. All of the code for the
behavioural planner is contained in behavioural\_planner.py.

To do this, you will first implement the helper functions
get\_closest\_index() and get\_goal\_index(). These will let the
behavioural planner know where it is relative to the global path, and to
compute the current goal point from the global path. Once these are
done, you will then implement the transition\_state() function, which
contains the behavioural state machine logic. The required details about
each of these functions are given in the code comments. Please complete
all TODOs for this assignment.

Path Generation
---------------

For the path generation section of the project, the majority of the
mathematical code for generating spiral paths is given to you. However,
you will need to compute the goal state set (the set of goal points to
plan paths to before path selection) using the get\_goal\_state\_set()
function, as well as some of the path generation helper functions. In
particular, you will implement thetaf(), which computes the yaw of the
car at a set of arc length points for a given spiral,
optimize\_spiral(), which sets up the optimization problem for a given
path. Finally, once the optimization is complete, the resulting spiral
will be sampled to generate the path. This functionality needs to be
implemented in sample\_spiral(). The required details about each of
these functions are given in the code comments in the files
local\_planner.py and path\_optimizer.py. Please complete all TODOs for
this assignment.

Static Collision Checking
-------------------------

For this part of the motion planner, we will be editing
collision\_checker.py. In particular, we're going to be implementing
circle-based collision checking on our computed path set using the
collision\_check() function. You will implement the circle location
calculation for each point on the path. For futher details, please refer
to the given code comments. Please complete all TODOs for this
assignment.

Path Selection
--------------

The path selection portion of the project involves you evaluating an
objective function over the generated path set to select the best path.
The goal of this section is to eliminate paths that are in collision
with static obstacles, and to select paths that both track the
centerline of the global path. To encourage robust obstacle avoidance,
we will also need to add a term that penalizes how close the planned
path is to other paths in the path set that are in collision with a
static obstacle. You will implement path selection in the
select\_best\_path\_index() function within collision\_checker.py. For
further details, please refer to the given code comments. Please
complete all TODOs for this assignment.

Velocity Profile Generation
---------------------------

The last step of the project is velocity profile generation. This
velocity planner will not handle all edge cases, but will handle stop
signs, lead dynamic obstacles, as well as nominal lane maintenance. This
is all captured in the compute\_velocity\_profile() function in
velocity\_planner.py. You will be implementing the physics functions at
the end of the file which will be used for velocity planning. For
further details, please refer to the given code comments. Please
complete all TODOs for this assignment.

Once you have completed a TODO for a given function, you can uncomment
it in "**module7.py**". After completing all TODOs, you should now be
ready to run the simulator.

Running the CARLA simulator
===========================

In one terminal, start the CARLA simulator at a 30hz fixed time-step:

**Ubuntu:**

``` {contenteditable="false" dir="ltr" data-language="sh" style="opacity: 1;"}
./CarlaUE4.sh /Game/Maps/Course4 -windowed -carla-server -benchmark -fps=30
```

**Windows:**

``` {contenteditable="false" dir="ltr" data-language="sh" style="opacity: 1;"}
CarlaUE4.exe /Game/Maps/Course4 -windowed -carla-server -benchmark -fps=30
```

Note that both the **ResX=\<pixel\_width\>** and
**ResY=\<pixel\_height\>** arguments can used to create a fixed size
window, if you find the simulation to run too slow. See the CARLA
installation guide for more details on how to use the arguments.

Running the Python client (and controller)
==========================================

In another terminal, change the directory to go into the
"Course4FinalProject" folder, under the "PythonClient" folder.

Run your controller, execute the following command while CARLA is open:

**Ubuntu**(use alternative python commands if the command below does not
work, as described in the CARLA install guide)**:**

``` {contenteditable="false" dir="ltr" data-language="sh" style="opacity: 1;"}
python3 module_7.py
```

**Windows**(use alternative python commands if the command below does
not work, as described in the CARLA install guide)**:**

``` {contenteditable="false" dir="ltr" data-language="sh" style="opacity: 1;"}
python module_7.py
```

The simulator will begin to run if the module\_7.py client connects to
the server properly. It will open two new feedback windows (unless
live\_plotting is disabled - see the **changing the live plotter refresh
rate** section below for more details), one of which shows the top-down
trajectory and the other which shows the controls feedback.

Changing the live plotter refresh rate
--------------------------------------

If the simulation runs slowly, you can try increasing the period at
which the live plotter refreshes the plots, or disabling the live
plotting altogether. Disabling the live plotting or changing its refresh
rate does not affect the plot outputs at the end of the simulation.

To do this, edit the **options.cfg** file found in the
"Course1FinalProject" folder for the relevant parameters. The following
table below explains each option:

  Parameter                Description                                                                                                           Value
  ------------------------ --------------------------------------------------------------------------------------------------------------------- ------------
  live\_plotting           Enable or disable live plotting.                                                                                      true/false
  live\_plotting\_period   Period (in seconds) which the live plot will refresh on screen. Set to "0" for an update every simulation timestep.   [seconds]

Evaluating the simulation results
=================================

This will then start the simulation and will run your developed Python
client. Once you reach the end of the scenario, the Python client will
output controller\_output/trajectory.txt and
controller\_output/collision\_count.txt. You should submit both of these
files to Coursera for grading. You will be graded on generating a
collision-free path to the goal, without deviating too greatly from the
waypoints both in terms of speed and velocity. You will also need to
come to a complete stop in the designated stop region before the stop
sign as well.

### How to submit {.c-title}

When you're ready to submit, you can upload files for each part of the
assignment on the "My submission" tab.

Close

-   Multiple Comments

Discussions {.rc-ForumsTabBody__title}
-----------

-   ### Mistake in velocity\_planner.py {.rc-ForumsPanelItem__title}

    Line 234:

    ``` {contenteditable="false" dir="ltr" data-language="python" style="opacity: 1;"}
    vi = calc_final_speed(vf, -self._a_max, dist)
    ```

    must be changed to:

    ``` {contenteditable="false" dir="ltr" data-language="python" style="opacity: 1;"}
    vi = calc_final_speed(vf, self._a_max, dist)
    ```

    because we are solving the inverse problem here. This prevented me
    from submitting the solution successfully from the first try (the
    velocity planner went haywire at some point and made the car stop
    half a meter before the accepted zone, which still looked ok
    visually). Also, deceleration\_distance should be clamped to zero
    (the original code can make it become negative, affecting further
    calculations in this method).

    0 Replies

-   ### Stuck getting past stop sign {.rc-ForumsPanelItem__title}

    What's the conceptual approach to the stop sign scenario? I
    understand the trapezoidal decelerate profile, which uses a stopping
    buffer distance to stop a few meters ahead of the stop sign. Once
    the vehicle is stopped, however, how does the vehicle move past the
    stop sign? The function "check\_for\_stop\_signs" returns true since
    the car is behind the stop sign line, and I don't understand how to
    move past it.

    What is the desired behavior when the vehicle has been in
    STAY\_STOPPED for a long time but then still detects a stop sign
    along the path? Could someone explain their approach to getting past
    the stop sign line?

    8 Replies

-   ### module\_7.py issue {.rc-ForumsPanelItem__title}

    After uncommenting the local planner code in module\_7.py, there is
    one attribute from LocalPlanner which is not defined
    'lp.\_prev\_best\_path'. How to declare that in the LocalPlanner
    class? I get the following error whenever I run the code:

    AttributeError: 'LocalPlanner' object has no attribute
    '\_prev\_best\_path'

    2 Replies

[](https://www.coursera.org/learn/motion-planning-self-driving-cars/discussions/forums/HTre__RIEei9qgqM89SsXg)

External Link

View all discussions

### Confirm Navigation

Are you sure you want to leave this page?

Stay on this Page

  

Leave this Page
