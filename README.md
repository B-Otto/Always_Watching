# Always_Watching
This project builds a model using Keras ConvLSTM2D layers to detect crime in surveillance videos

## What's the Problem?

By the end of 2021 it was estimated that over one billion security cameras would be in use world wide. Around half of those cameras can be found in China, but the United States is not far behind in surveillance cameras per-capita (Cosgrove, 2019). Between government surveillance, private companies, and citizens protecting their own homes, it's become a way of life to assume we are often, if not always being watched. One study finds that in a commute of 29 miles, a US citizen may turn up on as many as 20 cameras and then be filmed an additional 40 times each week around their office (Melore, 2020). I drive mainly interstates and work at the airport, so I can confirm this!

The problem becomes, who monitors these cameras? Do we have enough eyeballs to cover each camera every minute? Do we need help from artificial intelligence? One secutity company polled their customers and found that 15% never even looked at their security footage, instead finding comfort that if a crime was reported, they could rewind (Pro-Vigil, 2022) 

But what if an employee is stealing, the business may not know until they've taken thousands in assets. Or, what if a person is abducted in the back of a warehouse that has unmonitored cameras, the clock is ticking to save that person. When will the victim be reported missing? How long will it take for police to connect that warehouse to them. How long will it take for the warehouse owner to turn over the footage. At that point, how many hours of footage need to be scoured to find the scene?

Can we build a machine learning model that can watch, interpret human actions, and correctly relay that information to authorities?

This is the problem I dove into. 



## Angle of Attack

I obtained a dataset from the University of Central Florida's Center for Research in Computer Vision: https://www.crcv.ucf.edu/projects/real-world/. This dataset contains 1900 videos averaging around 30 seconds each. The videos are classified into 13 labels, ranging from normal activity to burglary to road accidents. This dataset was free to download and was already in MP4 format for processing. 

Because I wanted to build and improve a model, I knew processing time and power would be a concern for all 1.7 million frames. Because of this, I cut the dataset down to just 9 categories: No Crime, Burglary, Explosion, Fighting, Robbery, Shooting, Shoplifting, Stealing, and Vandalism. 
 
I got set loading my data and visualizing it. I wanted to see a histogram of the label categories so that I knew if my dataset would be heavily skewed. It did not appear to be. I then used a column of random numbers in the dataframe to separate the data into train, validation, and test sets. I then extracted the frames while also filtering for frames that were mostly black or white- such as logos at the beginning and end of the video, reshaped and resized frames, preserved the directory so labels could be inferred, and saved the list of frames into a file for later retrieval. I then created a dataset using the frames extracting pixel values and labels. I input them into my chosen model, ConvLSTM2D, and tried to optimize it. 



## What is a ConvLSTM2d layer?

I considered using a classic Convolutional Neural Network for this problem, but I knew that once the frames were split, it would be hard to classify the frames correctly without taking into accout the order that in which the action happened. Because of this, I knew I had to include a time sequence element into the model. The ConvLSTM2D model is the best of both worlds. 

The Convolutional portion of the network uses filters to scroll over the frames to slowly recognize patterns, edges, etc. from the frame. The Long-Short Term Memory portion of the model gives importanceto the action sequence to predict labels on new data. I've seen examples of ConvLSTM2d being used for human action recognition (https://www.youtube.com/watch?v=QmtSkq3DYko) and also movie genre prediction (Xavier, 2019). This seemed like it could do the job. 
