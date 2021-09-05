# Human Pose Estimation Project
Code repository for AMI Lab 2021 Summer Undergraduate Research Program

## File Directory
### pretrained model & checkpoints
```sh
models/model_A.py
models/model_A_checkpoint.pt

models/model_B.py
models/model_B_checkpoint.pt
```
## Installation instructions
### model A
```sh
conda env create --file venv/model_A.yaml
conda activate model_A

# Neural-Renderer-Pytorch library has some dependency issues with our project, 
# thus manually fix some codes, then build source. 
# Do not use 'pip install neural_renderer_pytorch' !!

git clone https://github.com/daniilidis-group/neural_renderer.git

cd neural_renderer/neural_renderer/cuda

# Find all 'AT_CHECK' in the below codes, then edit them to 'AT_ASSERT'

vi create_texture_image_cuda.cpp 
vi load_textures_cuda.cpp 
vi rasterize_cuda.cpp 

# After modifying above codes, then build the source manually on your "GPU Device"
# At /path_to_your_project_dir/neural_renderer

pip install . # (or python setup.py install)
```

### model B
```sh
conda env create --file venv/model_B.yaml
conda activate model_B

# Neural-Renderer-Pytorch library has some dependency issues with our project, 
# thus manually fix some codes, then build source. 
# Do not use 'pip install neural_renderer_pytorch' !!

git clone https://github.com/daniilidis-group/neural_renderer.git

# build the source manually on your "GPU Device"
# At /path_to_your_project_dir/neural_renderer

pip install . # (or python setup.py install)
```

## Evaluation
### model A
```sh
# models/__init__.py
# commented out Line 4 and save Line 5 
 4 #from .model_B import my_model
 5 from .model_A import MY_MODEL

# eval.py
# commented out Line 29 and save Line 31
 29 #from models import hmr, SMPL, my_model
 31 from models import hmr, SMPL, MY_MODEL
 
 # After import appropriate pretrained model, execute evaluation code
 python eval.py --dataset=mpi-inf-3dhp --checkpoint=models/model_A_checkpoint.pt --model=model_A
```
### model B
vise-versa
```sh
# models/__init__.py
# commented out Line 5 and save Line 4 
 4 from .model_B import my_model
 5 #from .model_A import MY_MODEL

# eval.py
# commented out Line 31 and save Line 29
 29 from models import hmr, SMPL, my_model
 31 #from models import hmr, SMPL, MY_MODEL
 
 # After import appropriate pretrained model, execute evaluation code
 python eval.py --dataset=mpi-inf-3dhp --checkpoint=models/model_B_checkpoint.pt --model=model_B
```




