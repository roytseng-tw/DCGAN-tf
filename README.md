# DCGAN in Tensorflow with original paper implementation
This implementation use the 'Hook' classes in Tensorflow 1.0.0 or newer, which is really convenient.  
In [carpedm20](https://github.com/carpedm20/DCGAN-tensorflow)'s implementation,unbalanced update of G and D
is required to get good results. This is most probably due to the way of feeding input batch.
In original paper, new *z's* (random vector) and new *real images* are sampled for each update of D or G.
However, carpedm20 uses the same inputs for a whole update iteration of D and G, that is sampling only once before training D ```d_step``` times and then G ```g_step``` times.

I implement both training strategies.
The original one is refered as **strategy1**, and carpedm20's is refered as **strategy2**.
By defautl, I use strategy1, but you can explicitly assign it by setting ```--training_strategy=[1|2]```.

## Prerequisite
Python3  
Tensorflow>=1.0.0  
Scipy
Test

## Dataset
This code was tested on `celebA`. Of course you can try on other datasets.
- Download celebA dataset
(use the [donwload.py](download.py) script borrowed from [carpedm20](https://github.com/carpedm20/DCGAN-tensorflow/download.py))
```bash
python download.py celebA
```
Downloads will put under ```./data```.

## Training
We offer two strategies to train the DCGAN model.
- Strategy 1 (Just use the default settings)
```bash
python main.py 
```
- Strategy 2
```bash
python main.py --training_strategy=2 --g_step=2 
```

## Testing
Not implement yet.

## Training process visualization
Two strategies both produce similar results.
- Strategy1

  ![Strategy1](images/strategy1_training.gif)

- Strategy2

  ![Strategy2](images/strategy2_training.gif)

## Make training sample images to GIF
```bash
python make_gif.py /dir/to/images output_path.gif 
```
