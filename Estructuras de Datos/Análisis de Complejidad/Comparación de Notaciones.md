Below is a table comparing Big O notation, Ω (Omega) notation, and θ (Theta) notation:

|Notation|Definition|Explanation|
|---|---|---|
|Big O (O)|f(n) ≤ C * g(n) for all n ≥ n0|Describes the upper bound of the algorithm's running time. Used most of the time.|
|Ω (Omega)|f(n) ≥ C * g(n) for all n ≥ n0|Describes the lower bound of the algorithm's running time . Used less|
|θ (Theta)|C1 * g(n) ≤ f(n) ≤ C2 * g(n) for n ≥ n0|Describes both the upper and lower bounds of the algorithm's ****running time****. Also used a lot more and preferred over Big O if we can find an exact bound.|

In each notation:

- $f(n)$ represents the function being analyzed, typically the algorithm's time complexity.
- $g(n)$ represents a specific function that bounds $f(n)$.
- $C$, $C1$​, and $C2$ are constants.
- $n_0$ is the minimum input size beyond which the inequality holds.