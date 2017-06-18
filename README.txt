::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
INSTALLATION GUIDE:

1) Install Caffe on Windows
https://github.com/BVLC/caffe/tree/windows

2) Install Deep Dream
https://github.com/google/deepdream/blob/master/dream.ipynb

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
PRODUCING DREAMS:

1) First we need to generate frames from a video
- On Ubuntu, install 'avconv'
- in 'Terminal' run
	./1_movie2frames.sh avconv [original_video] [frames_directory] jpg
	
2) Second step is dreaming with DeepDream
- On Windows in 'cmd' run the following command

python 2_dreaming_time.py -i frames -o "processed/output_folder" --gpu 0 -it jpg --model_path "models/Googlenet fine-tune/" --model_name googlenet_boris_iter_350000.caffemodel -l inception_5b/pool_proj -b "loop"

-i [folder] ... where the input frames are
-o [folder] ... where to store processed frames
-gpu 0 ... use graphic card True (1 for false)
-it jpg ... the picture type of the frames
--model_path [folder] ... where the model is located
--model_name [name.caffemodel] ... name of the caffemodel
-l [name of layer] ... on which layer of the neural network to run the DeepDream on (layer names can be found in solver.prototxt, layer from inception_4a on give interesting results)
-b "loop" ... blending of the frames will go from 50% to 100% and the reset

more can be read at:
https://github.com/graphific/DeepDreamVideo

3) Third step is converting the processed frames back to a video
- On Ubuntu in Terminal (inside the folder where the frames are)
avconv -framerate 30 -i %08d.jpg -c:v libx264 -profile:v high -crf 20 -pix_fmt yuv420p output_name.mp4

-framerate [30] ... how many fps was the original video shot in

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
An example of a processed video can be found at:

https://drive.google.com/file/d/0B2SntE-mtIhdN2gzbDFmOFg0VnM/view

(You have to download it for original 720p quality)