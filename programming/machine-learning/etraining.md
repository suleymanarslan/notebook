 # Retraining
 
 ## Creating model with `retrain.py`
 
 Download `retrain.py`:
 
 ```bash
 $ curl -LO https://github.com/tensorflow/hub/raw/master/examples/image_retraining/retrain.py
 ```
 
 Run it on a folder of training data:
 
 ```bash
 $ python retrain.py --image_dir ~/flower_photos
 ```
 
 ## Using the model
 
 Download `label_image.py`: 
 
 ```bash
 $ curl -LO https://github.com/tensorflow/tensorflow/raw/master/tensorflow/examples/label_image/label_image.py
```
Run it on the saved model files:

```bash
python label_image.py \
--graph=/tmp/output_graph.pb --labels=/tmp/output_labels.txt \
--input_layer=Placeholder \
--output_layer=final_result \
--image=$HOME/flower_photos/daisy/21652746_cc379e0eea_m.jpg
```
