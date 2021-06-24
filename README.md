# Keras_retinanet_on_custom_dataset_for_object_detection
## Instructions to use-
1. Clone the repository.
2. Clear the images and annotation directory present in the dataset directory.
3. place all the images of the custom dataset into the dataset/images directory.
4. Now,create annotation file for each images and place all annotation xml files in dataset/annotations directory. Which will be in xml format. LabelImg is one of the tool which can be used for annotation.
5. Then we have to set the config file custom_dataset_config.py inside config directory. Here set the path for annotation, image, train.csv files and also set the path where the classes.csv have to be saved. TRAIN_TEST_SPLIT value will split the data for training and testing.
6. Run requirements.txt file and install the dependencies.
7. create train.csv, test.csv and classes.csv by using build_dataset.py inside this directory. Run the following command inside the directory-
    `python build_dataset.py`
8. The datas inside train.csv and test.csv will be in the following format-
    `<path/to/image>,<xmin>,<ymin>,<xmax>,<ymax>,<label>`
9. classes.csv will be in following format-
   `label, index`
10. Download the pretrained weights on the COCO datasets with resnet50 backbone from this link-https://github.com/fizyr/keras-retinanet/releases/download/0.5.1/resnet50_coco_best_v2.1.0.h5
11. Run setup file by following command-
   `python setup.py build_ext --inplace`
12.Start the training by following command-
`python keras_retinanet/bin/train.py --weights resnet50_coco_best_v2.1.0.h5 --steps 150 --epochs 40 --snapshot-path snapshots --tensorboard-dir tensorboard csv dataset/train.csv dataset/classes.csv --val-annotations dataset/test.csv`
13.The model have to be converted in a format which can be used for prediction. For this run one of the following command-
`python keras_retinanet/bin/convert_model.py <path/to/desired/snapshot.h5> <path/to/output/model.h5>`
## To start detection-
Set model_path, video_path, output_path and labels_to_names values in the people_detection_video.py Run the following command.
`python people_detection_video.py`

An output video will be saved in the mentioned path.
Also detecting from image is done by run the following command.
`python people_detection_image.py`
