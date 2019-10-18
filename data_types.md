# Data types within the Prism.AI system

### Artifacts

1.  ### Video
![](https://docs.google.com/a/prism.com/drawings/d/slY5OPa2NitB4fWLbWOmAzQ/image?w=470&h=45&rev=4&ac=1&parent=1-CfcVKfhJ-EVWUaLbHG7kdzVsxN-AtClM1EJ1zkKq8Q)
Original, low quality (flipbook), or summary video

Metainformation:
-   Width   
-   Height    
-   Fps 
-   Frame number
-   Start and end timestamps

2.  ### Background
   
TBD

3.  ### Image/Object representation
    
![](https://docs.google.com/a/prism.com/drawings/d/sMfcaXuzNDSNWuX5OAjswSA/image?w=513&h=167&rev=276&ac=1&parent=1-CfcVKfhJ-EVWUaLbHG7kdzVsxN-AtClM1EJ1zkKq8Q)

Object representations are images that are designed for two purposes
-   Representing object on screen with enough context around to be recognizable
-   Providing uncropped object image that will seamlessly blend back on original frame
-   Saving bandwidth by not sending ‘background data that is not changed between frames or is irrelevant for application
    

Original video frames are object representations, images are also object representations’

Metainformation:
-   Normalization parameters
-   Bottom Left position X,Y
-   Width, Height
-   Original frame Width, Height
-   Start and end timestamps (that usually should be identical)
-   Object ID’s of objects represented
    
4.  ### Summary video/tapestry
    
Special case of video/image above, produced for final consumption. This affects object lifecycle only (typically very short 10m to 1 day)

5.  ### Object Bounding boxes 
![](https://docs.google.com/a/prism.com/drawings/d/stq5i5C2XUovzqheydape-Q/image?w=329&h=205&rev=135&ac=1&parent=1-CfcVKfhJ-EVWUaLbHG7kdzVsxN-AtClM1EJ1zkKq8Q)

Bounding boxes are supposed to be ‘object localization’. Goal is to leave enough context for object to be recognizable, and removing visible parts of another objects that may lead to different classification.

Metainformation:
1.  Bottom Left position X,Y (global or within objectRepr?)  
2.  Width, Height  
3.  Original frame(objectRepr?) Width, Height
4.  Start and end timestamps (that usually should be identical)  
5.  Object ID of object represented
    
  
6.  ### Tracks
![](https://docs.google.com/a/prism.com/drawings/d/sZ4aES9_8vBuxpIW64Ap93A/image?w=624&h=166&rev=216&ac=1&parent=1-CfcVKfhJ-EVWUaLbHG7kdzVsxN-AtClM1EJ1zkKq8Q)

Tracks are connecting positions of the same object within different frames on video

Metainformation:
1.  Start and end timestamps   
2.  Object ID of object represented   
3.  Array of track positions within [start, stop] time range
    
In form of [ x_pos, y_pos, time_delta_in_ms]

7.  ### Labels/Tags  ![](https://docs.google.com/a/prism.com/drawings/d/sQwzaFxfj0MHl7aTGd5dlTQ/image?w=624&h=292&rev=138&ac=1&parent=1-CfcVKfhJ-EVWUaLbHG7kdzVsxN-AtClM1EJ1zkKq8Q)
Labeling services may return either just list of labels or list of labels and bounding boxes associated with each label. General object classification usually returns just labels while text or face detect labels + bounding boxes.

Metainformation:
 1. Start and end timestamps (that usually should be identical)
 2. ObjectRepr id
 3. List of [label, confidence] pairs with optional bounding boxes   
 
8.  ### Time series data
![](https://docs.google.com/a/prism.com/drawings/d/s3cPbJD6g0wNSlMOFMYc9nw/image?w=600&h=342&rev=107&ac=1&parent=1-CfcVKfhJ-EVWUaLbHG7kdzVsxN-AtClM1EJ1zkKq8Q)
Time series are designed to store various structured data that does not conform to image/video restrictions (i.e (pixel) value is outside of 0..255 range, double/float or >2 dimensions). It can be as simple as 1d data like time based counts or as complex as SIFT descriptor for specific image position. Position itself is optional and may be omitted. Text annotations are also forms of time series data.

Metainformation:
1.  Start and end timestamps
2.  Data dimensions (numpy format)
3.  Array of data within [start, stop] time range
In form of [ [flat_data_array], time_delta_in_ms]
4.  (optional) Array of data positions within [start, stop] time range
In form of [ x_pos, y_pos, time_delta_in_ms]

9.  ### Event
    
Event is arbitrary grouping of artifacts(above). Artifacts can be manually selected or grouped based on criteria like time range. This can be user upload session, user defined time range, user defined set of artifacts or some rule, usually something like ‘track crossed tripwire’ or ‘track is longer than 30 sec and object label is ‘moose’’


# Data Sources
![](https://docs.google.com/a/prism.com/drawings/d/sTSGByyVg-ew5q9o_ruDgVw/image?w=624&h=435&rev=232&ac=1&parent=1-CfcVKfhJ-EVWUaLbHG7kdzVsxN-AtClM1EJ1zkKq8Q)

  
# Data Slices

1.  ### Time slice
![](https://docs.google.com/a/prism.com/drawings/d/s16MXGpNek_v73mCdAflDPA/image?w=488&h=145&rev=63&ac=1&parent=1-CfcVKfhJ-EVWUaLbHG7kdzVsxN-AtClM1EJ1zkKq8Q)
Most common representation of sequential frames within same feed

2.  ### Feed slice/Channel slice
![](https://docs.google.com/a/prism.com/drawings/d/siMv3GNkmJeOOGLWZGcyg5A/image?w=624&h=215&rev=65&ac=1&parent=1-CfcVKfhJ-EVWUaLbHG7kdzVsxN-AtClM1EJ1zkKq8Q)
Same timestamp but different feeds
