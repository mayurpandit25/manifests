DEPLOYMENT STRATEGIES IN KUBERNETES

1.Rolling Update
    a stategy that create a new versions of a pod one after the another.it means that we dont get the downtime while updating.

ex.old app is replaced slowly one by one
1.one old pod stops
2.one new pod starts
3.users dont notice anything 

===============================================================================================================================

2.Recreate strategy
   a strategy that terminates the old versions and create the new versions. so we get downtime while updating and generally we 
  dont use these strategy in production.

ex.stops everything -> start the new app
1.All old pods stop first
2.New pods start after that
3.Use for testing or learing

===============================================================================================================================

3.Blue-Green Deployment
   A strategy that creates the new versions alongside with the old versions and then switch the traffic. We use these strategy 
  in the production.

ex.two apps running side by side
1.blue -> old app
2.green -> new app
3.Use for the critical applications

===============================================================================================================================

4.Canary Deployment
   A strategy that releases new versions to a subset of user then procced to full rollout.

ex.test new app with few users first
1.90% users -> old app
2.10% users -> new app

===============================================================================================================================

5.A/B Testing
   These strategy shows the different versions to different users

1.some users see version-1
2.some users see version-2
3.compare results
4.Use for experiment and features

===============================================================================================================================

What is maxSurge and maxUnavailable

1.maxSurge:-
   maxSurge can controls how many extra pods are created during update

2.maxUnavailable
   maxUnavailable controls how many pods can be unavailable during rolling-update in kubernetes

==============================================================================================================================
