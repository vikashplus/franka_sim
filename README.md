# Franka
Franka panda mujoco models

franka_panda.xml           |  bi-franka_panda.xml |
:-------------------------:|:-------------------------:
![Alt text](franka.png?raw=false "franka") | ![Alt text](bi_franka.png?raw=false "bi-franka")  |

# Model edits
Franka Panda is emerging as a platform of choice for many labs owing to its price point and hardware stability. However, its well acknowledged that its kinematics, default zero positions, and joint limits are slightly unconventional for common usage. To avoid these unconventional issues, a few adjustments are provided in this repo to help avoid common pitfalls. Notably
1. Joint adjustments are applied to adapt the default position of the arm towards a more natural posture. Especially an offset of `-pi/2` is applied to joint6 and `-pi/4` is applied to joint7.
2. The zero position of joint4 results in the gimble lock configuration for the arm. The range of joint4 is carefully adjusted (reduced a bit). This small edit is very important to avoid gimble lock configurations. (Owing to the official design of the model at its default configuration, the model during load will get initialized a bit outside of joint limits. It will quickly snap inside the limits post-initialization. This is expected and normal)
3. Joint limits are adjusted a bit to avoid hitting the joint limits during operation with the hardware.

# Model adaptation while working with the hardware
The above adaptations, however, minors, are a result of the practical wisdom accumulated by operating >30 Franka robots, over >1000s of hours across>10 projects. The edits present in this model result from practical experience and contain conventional wisdom that is commonly missing in academic papers. When working with the hardware, while most edits will be silent, users will **need** to adjust for the offset on joint6 and joint7 in their hardware wrapper/ sim2real calibrations. An example of this adjustment can be found in [here in RoboHive](https://github.com/vikashplus/robohive/blob/main/robohive/envs/arms/franka/assets/franka_reach_v0.config). Users are encouraged to use their solution.

# Acknowledgements
Robot's Meshes and specs are from

1. https://github.com/frankaemika/franka_ros
1. https://frankaemika.github.io/docs/control_parameters.html#constants