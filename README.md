# Velogames solver

A script to calculate the optimal team that could have been chosen for a given race in [Velogames fantasy cycling](https://www.velogames.com/)

This script uses the [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/) library to scrape rider data, and the [Pyomo](http://www.pyomo.org/) optimisation library to construct and solve a linear program described below

In Velogames fantasy cycling, you must select a team of 9 riders, each with a specific cost based on their expected performance, spending no more than 100 points. 

Each rider is classed as either an All-Rounder, a Climber, a Sprinter or is Unclassed. A team must contain 2 All-Rounders, 2 Climbers, 1 Sprinter and 3 Unclassed riders. The 9th selection can be from any class.

At the end of the race, each rider will have accumulated a score based on their performance, and the aim is to pick a team with the highest combined score at the end of the race.

The optimisation problem can be stated as:

<img src="https://render.githubusercontent.com/render/math?math=maximise \sum_{j=1}^{n} x_j y_j">

<img src="https://render.githubusercontent.com/render/math?math=s.t.">

<img src="https://render.githubusercontent.com/render/math?math=\sum_{j=1}^{n} x_j=9">
<img src="https://render.githubusercontent.com/render/math?math=\sum_{j=1}^{n} c_j z_j \leq 100">
<img src="https://render.githubusercontent.com/render/math?math=\sum_{j=1}^{n} c_j a_j \geq 2">
<img src="https://render.githubusercontent.com/render/math?math=\sum_{j=1}^{n} c_j c_j \geq 2">
<img src="https://render.githubusercontent.com/render/math?math=\sum_{j=1}^{n} c_j s_j \geq 1">
<img src="https://render.githubusercontent.com/render/math?math=\sum_{j=1}^{n} c_j u_j \geq 3">

where <img src="https://render.githubusercontent.com/render/math?math=j=1...n"> is the set of all riders

$x_j$ is a binary decision variable denoting if rider $j$ is chosen (1 for chosen, 0 for not chosen)

$z_j$ and $y_j$ are the cost and score of rider $j$ respectively

$a_j$, $c_j$, $s_j$ and $u_j$ are binary values denoting if rider $j$ is an All-Rounder, Climber, Sprinter or Unclassed respectively
