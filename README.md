# dp2026_auto_aim
The demo of CUHKsz auto aim algorithm.

## 📖 Getting Started
Recommend Environment
```bash
nvcc --version # 12.6
dpkg -l libcudnn9 # cudnn 9.3
dpkg-query -W tensorrt # TensorRT 10.3
cmake --version # 3.24.0
```

You can follow the following instructions to get this env:

1. Go to docker folder to build the env.
2. In the docker env, install the dependencies.

Dependence



## 🕹️ Play!
* Visualize the model in drake/mujoco

  * drake

      ```bash
      # example
      python scripts/visualize_model_drake.py kuavo/s46/biped_s46.urdf biped_s46
      ```

  * mujoco

      ```bash
      # example
      python scripts/visualize_model_mujoco.py kuavo.yaml
      ```
      
* Run HLIP+CIMPC algorithm in drake/mujoco+drake

  * drake

      ```bash
      # example
      python demo/drake/achilles_se3/main.py --with_arms
      ```

  * mujoco+drake

      ```bash
      # example
      python demo/mujoco/achilles/main_walk.py 