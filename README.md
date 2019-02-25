# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---
## Relection
### Describe the effect each of the P, I, D components had in your implementation.
P component, which is short for Propotional component, is used to calculate the steer angle with the product of Tau_P and CTE, where Tau_P is the hyperparameter and CTE is the current CrossTrack Error. Since the steer angle will be output to the vehicle the next cycle, and the CTE is the current value, the P component will cause the steer angle oscillatted. The larger the Tau_P value, the more angle oscillated.

D component, which is short for Derivative component, is used to calculate the steer angle with the product of Tau_D and d_CTE, where tau_D is the hyperparameter and d_CTE is the differential of CrossTrack Error. The differential of CTE represents the trend  of CTE,  and since the CTE is continuous, the D component is meaningful.When the CTE is decreasing as the result of P, the d_CTE will be negative, and D component will weaken the effect of P component; and When the CTE is increasing, the d_CTE will be positive, and D component will enhance the effect with the P component. The larger the Tau_P value, the more weaken or enhance effect produced.

I component, which is short for Integral componant, is used to calculate the steer angle with the product of Tau_I and i_CTE, where tau_I is the hyperparameter and i_CTE is the integral of CrossTrack Error from the beginning. i_CTE represents the cumulative error from the start to current time. And if the system bias exists, it will also cumulate all the time and can not be eliminated. Therefore, I component may be used for eliminating the system bias. But the Tau_I will be always a very small value.

### Describe how the final hyperparameters were chosen.
The parameter is manual  tuned. As suggested from previous lessons, first I choose Tau_P to tune and set the Tau_I and Tau_D to zero, and to avoid frequently compiling, these parameters are passed to the  `int main(int argc, char * argv[])`. When Tau_P is -0.05, the vehicle can make through most of the road except the two sharp turns. Then I start to increase the value of Tau_D. And when the Tau_D is -1.5, the vehicle can make through the sharp turns. And as adviced by the *Note*, I set the throttle to 0.1 when the angle is more than 10 degrees to slow down a little bit when turning. the Tau_I is left to 0 since we have already make it.

