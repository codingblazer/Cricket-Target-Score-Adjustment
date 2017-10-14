# Model for Score Revision in International Cricket (T20 Matches)

In matches interrupted by bad weather in International Cricket, the target score for batting-second team is readjusted using DuckWorth-Lewis-Stern Model. But this model has failed many times by giving unsatisfactory results. The detailed analysis on weaknesses of this model and other proposed models will be discussed soon (with supported examples where they fail).

This project proposes an alternate algorithm for revision of scores in International Cricket. This method is essentially an algorithm based on following argument :

“The present models so far uses the past matches data to adjust the target score. But this is against the very notion of Fair Cricket Game. **The performance of team in present match should not be judged by their performance in past.** Every match is an independent match with no relation with past whatsoever. It resembles a lot with us in sense that everyday of our life is a different day.”

## Algorithm :

**Concept :** 

Unlike present models, my algorithm considers just the present match and uses no references to past. For this, we need criterion that remains same throughout the match with respect to team - The performance. Every team at any point of match performs the same i.e. = the best they can with respect to them.
That’s why, I will take team performance for the overs completed before the rain interruption to predict the performance in lost overs.

How to measure performance ?

The main factors on which we can tell how the team performed for specific period of overs are Runs and Wickets.

> Runs/specific overs = + Run Rate 


> Wickets lost in specific overs = - Wicket fall rate (since losing wickets means negative performance)

Now considering that the model is devised for T20 format, we know that the wickets are less important in this format and hence in the performance equation, we will give less weightage to wickets.

> Performance equation = f(Run rate, Wickets)


BUT wait !! Though the team performs the same with respect to them = their best, but their actual performance varies due to variety of factors like wickets, etc.
Thus we will find the average rate of change of performance of the team for already played overs.

> Average Rate of change of Performance if team in given overs, R = delta(Performance) in given  overs

Now, the main mathematical approach is to find the R for team1 and team2 during the phase1. Let it be R1P1 and R2P1 respectively. Let’s calculate the R for team1 during the phase2 and let it be R1P2.

Now fractional change of R while transition from phase1 to phase2 will be 

> Transition ratio, T = R1P2/ R1P1

Now, what do we actually want to have a fair match ? We want that we somehow equalize the team1 and team2 during Phase2. But it also depends on the team situation (wickets remaining, run rate) while they are transiting from phase1 to phase2. Thus we can say that Transition ratio, T must be same for team1 and team2 when they transmitted from phase1 to phase2.  

In other words, we are saying that : “ The amount of change that team1 faced while transition calculated on their performance till now (phase1) = amount of change that team2 will face 
While transition, again calculated on their performance till now (phase 1).

Other Considerations :

Since Team1 didn’t knew about the rain during their innings, they should be compensated accordingly. This is because the Team1 would have strategized to play faster in beginning if they knew about the rain. Since Team2 know about the rain in their innings, they could change strategy to play faster.

	How to best take this into consideration ??

Since Team2 is changing their strategy to play faster in the Phase3 of their inning, we should only take this into account for Phase3 i.e. This should be in proportion to the number of overs in Phase3.
Example => If only 13 balls are left, we should not compensate heavily as it can turn match strongly in favor of Team1 => This supports my above statement that for less number of balls remaining, we should compensate less.

Compensation for Wickets to Team1 => Team1 could have lost some wickets during phase2 but since phase2 never occured for Team2, they didn’t lost any wickets. Even if Team1 didn’t lose any wickets in Phase2, we can safely say that they must not have taken too many risks (team avoid risky runs to protect their wickets). Because of this, they were always performing with fear of losing wickets.

Thus they should be definitely be compensated for this. 
