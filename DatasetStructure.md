# Dataset Structure


The Sigma Bench dataset consists of 85 _task execution sessions_ (or in short _sessions_), each in its own folder. Each session corresponds to an attempt to execute a task by one of the participants (regardless of whether they were successful or not). Each session directory is named in the format __`{yyyymmdd}-{hhmmss}`__, capturing the date and time when the task execution session started, e.g. 20250228-134800. 

Each session directory has a set of subdirectories containing the various data streams for that session, as described in the table below. Clicking the blue links in the left column will send you to a description of the data format/representation in that particular directory.

| Directory                     | Description |
|-------------------------------|-------------|
| [audio](#audio) | The system and user audio |
| [camera_intrinsics\color](#camera_intrinsics) | Intrinsics for the color camera  |
| [camera_intrinsics\depth](#camera_intrinsics) | Intrinsics for the depth camera  |
| [camera_intrinsics\leftfrontgrayscale](#camera_intrinsics) | Intrinsics for the left-front grayscale camera  |
| [camera_intrinsics\rightfrontgrayscale](#camera_intrinsics) | Intrinsics for the right-front grayscale camera  |
| [camera_pose\color](#camera_pose) | 3D pose for the color camera |
| [camera_pose\depth](#camera_pose) | 3D pose for the depth camera |
| [camera_pose\leftfrontgrayscale](#camera_pose)                   | 3D pose for the left-front grayscale camera |
| [camera_pose\rightfrontgrayscale](#camera_pose)                   | 3D pose for the right-front grayscale camera |
| [eye_gaze](#eye_gaze)                      | Eye gaze tracking |
| [eye_gaze_at_interface](#eye_gaze_at_interface)         | Data indicating whether the user is gazing at the task panel interface |
| [hands](#hands)                         | Hand tracking data |
| [head_pose](#head_pose)                     | Head pose data |
| [image\color](#image)                         | Color camera images |
| [image\depth](#image)                         | Depth camera images |
| [image\leftfrontgrayscale](#image)                         | Left-front grayscale camera images |
| [image\rightfrontgrayscale](#image)                         | Right-front grayscale camera images |
| [task_execution_session_data](#task_execution_session_data)   | Task execution data, including session metadata, task recipe, user and system utterances, step and sub-step execution details  |
| [user_interface_state](#user_interface_state)          | Data on 3D positioning of the task panel user interface |


<a name="audio"></a>
### `audio` directory

The `audio` directory contains `.wav` files for the system and user audio. The `.wav` files following the following naming convention:

* __{`session_name`}.audio.system.{`start_time`}.wav__: Contains the system audio. The `session_name` indicates the name of the session, and the `start_time` indicates the start time of the audio stream, in [ticks](timing).

* __{`session_name`}.audio.user.{`start_time`}.wav__: Contains the participant (user) audio. The `session_name` indicates the name of the session, and the `start_time` indicates the start time of the audio stream, in [ticks](#timing).

<a name="camera_intrinsics"></a>
### `camera_intrinsics` directory

The `camera_intrinsics` directory contains one subdirectory for each camera (color, depth, left-front grayscale and right-front grayscale), and each of those contain a file called __{`session_name`}.camera_intrinsics.{`camera_name`}.tsv__, where `session_name` is the session name and `camera_name` is the name of the camera. The file stores data in a tab-separated values containing the [timestamp](#timing) for the datapoint and the corresponding intrinsics matrix, distortion parameters, focal length information, the principal point, etc. as described in detail below:

```text
Time    M₀₀         M₀₁  M₀₂         M₁₀  M₁₁         M₁₂         M₂₀  M₂₁  M₂₂  R₀         R₁        R₂  R₃  R₄  R₅  T₀  T₁  FL          FLₓ         FLᵧ         PPₓ         PPᵧ         D   W   H
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
637835897126152279 251.437...  0    160.242...  0    251.647...  168.953...  0    0    1    -0.282...  0.064...  0   0   0   0   0   0   251.542...  251.437...  251.647...  160.242...  168.953...  1   320 288
```

The first value represents the time for the datapoint, expressed in [ticks](#timing).

The next 9 values represent the 3×3 intrinsics matrix (M₀₀ - M₂₂). This transform converts camera coordinates (in the camera's local space) into normalized device coordinates (NDC) ranging from -1 .. +1.

The next 6 values represent the radial distortion parameters (R₀ - R₅).

The next 2 values represent the tangential distortion parameters (T₀, T₁).

The next value represents the focal length in pixels (FL).

The next 2 values represent the focal length separated in X and Y in pixels (FLₓ, FLᵧ).

The next 2 values represent the principal point in pixels (PPₓ, PPᵧ).

The next value is a boolean indicating whether the closed form equation of the Brown-Conrady Distortion model distorts or undistorts (D).

The final two values represent the image width (W) and height (H) in pixels.

<a name="camera_pose"></a>
### `camera_pose` directory

The `camera_pose` directory contains one subdirectory for each camera (color, depth, left-front grayscale and right-front grayscale), and each of those contain a file called __{`session_name`}.camera_pose.{`camera_name`}.tsv__, where `session_name` is the name of the session and `camera_name` is the name of the camera. The file stores data as tab-separated values where each line contains the [timestamp](#timing) for the datapoint, followed by the 4x4 pose matrix (in row-major order) as tab-separated fields. For example:

```text
Time    M₀₀       M₀₁        M₀₂       M₀₃       M₁₀       M₁₁       M₁₂        M₁₃        M₂₀        M₂₁       M₂₂       M₂₃       M₃₀ M₃₁ M₃₂ M₃₃
---------------------------------------------------------------------------------------------------------------------------------------------------------------
637835897126152279  0.768...  -0.013...  0.639...  0.147...  0.097...  0.990...  -0.097...  -0.011...  -0.631...  0.136...  0.762...  0.041...  0   0   0   1
```


<a name="eye_gaze"></a>
### `eye_gaze` directory
 
The `eye_gaze` directory contains a file called __{`session_name`}.eye_gaze.tsv__, where `session_name` is the name of the session. The file stores data as tab-separated values where each line contains the timestamps for the datapoint, followed by the values representing the 3D ray. For example:

```text
Originating Time    P[x]      P[y]       P[z]      V[x]      V[y]      V[z]      Calib
--------------------------------------------------------------------------------------
637835897125443909  0.547...  -0.710...  0.418...  0.267...  0.159...  0.990...    1
637835897132944315  0.547...  -0.712...  0.418...  0.267...  0.159...  0.960...    1
637835897135110505  0.548...  -0.712...  0.419...  0.297...  0.160...  0.960...    1
```

The first value represents the timestamp for the datapoint, expressed in [ticks](#timing).

The next 3 values represent the position (P[x], P[y], P[z]) of the gaze ray origin. 

The next 3 values represent the vector direction (V[x], V[y], V[z]) of the gaze ray. 

The last value indicates whether the eye gaze calibration is valid (1) or not (0).

<a name="eye_gaze_at_interface"></a>
### `eye_gaze_at_interface` directory

The `eye_gaze_at_interface` directory contains a file called __{`session_name`}.eye_gaze_at_interface.json__, where `session_name` is the name of the session. The file captures the set of time intervals within which the participant is gazing at the `Sigma` virtual use interface (either at the dialog history bubbles or at the task panel containing the steps and substeps). This information is captured in a `.json` format, as an array of time intervals, as illustrated below. The start and end time for each interval is expressed in [ticks](#timing).

```json
[
  {
    "StartTime": 638763761038578647,
    "EndTime": 638763761074912624,
  },
  {
    "StartTime": 638763761105913175,
    "EndTime": 638763761109579907,
  },
  ...
]
```

<a name="hands"></a>
### `hands` directory

The `hands` directory contains a file called __{`session_name`}.hands.tsv__, where `session_name` is the name of the session. The file stores data as tab-separated values where each line contains the timestamps for the datapoint, followed by the values representing the poses for the left and then right hand.

The first value represents the time for the datapoint, expressed in [ticks](#timing).

The next 417 values capture the left hand. The first of them is a flag indicating the active state for the hand. This is followed by sets of 16 doubles for each of the following 26 joints (416 values) capturing the 4x4 pose matrix for that joint (in row-major order), followed by 26 boolean values (0 or 1) for the valid state of each joint, followed by 26 boolean values (0 or 1) for the tracked state of each joint. Missing or invalid joint values are represented by NaN.

The next 417 values capture the right hand in the same manner. 

The 26 joints are in order:

- Palm
- Wrist
- ThumbMetacarpal
- ThumbProximal
- ThumbDistal
- ThumbTip
- IndexMetacarpal
- IndexProximal
- IndexIntermediate
- IndexDistal
- IndexTip
- MiddleMetacarpal
- MiddleProximal
- MiddleIntermediate
- MiddleDistal
- MiddleTip
- RingMetacarpal
- RingProximal
- RingIntermediate
- RingDistal
- RingTip
- PinkyMetacarpal
- PinkyProximal
- PinkyIntermediate
- PinkyDistal
- PinkyTip

<a name="head_pose"></a>
### `head_pose` directory

The `head_pose` directory contains a file called __{`session_name`}.head_pose.tsv__, where `session_name` is the name of the session. The file stores data as tab-separated values where each line contains the [timestamp](#timing) for the datapoint, followed by 16 values representing the 4x4 pose matrix (in row-major order) for the head, as tab-separated fields. 

<a name="image"></a>
### `image` directory

The `image` directory contains one subdirectory for each camera (color, depth, left-front grayscale and right-front grayscale), and each of those contain a file called __{`session_name`}.image.{`camera_name`}.{`timestamp`}.jpg__ (or __.png__), where `session_name` is the name of the session, `camera_name` is the name of the camera, and `timestamp` is the [timestamp](#timing) for the image. Color, and left and right grayscale camera images are available as .jpg files, whereas depth images are available as .png files. 

<a name="task_execution_session_data"></a>
### `task_execution_session_data` directory

The `task_execution_session_data` directory contains a file called __{`session_name`}.task_execution_session_data.json__, where `session_name` is the name of the session. The file stores information about the task execution session in a json format, including session metadata, the task recipe, information about the user and system utterances, and about the step and substep execution. An abbreviated example is shown below for illustration purposes:

```json
{
  "SessionName": "20250228-134800",
  "StartTime": 638763760864908807,
  "EndTime": 638763767801966097,
  "TaskName": "Make a notebook using a binding machine",
  "ShortTaskName": "Notebook",
  "ParticipantId": "9",
  "ParticipantTaskOrder": "1",
  "TaskCompletion": "Abandoned",
  "Slice": "A",
  "Task": {
    "Name": "Make a notebook using a binding machine",
    "Steps": [
      {
        "Label": "1",
        "Description": "Prepare the binding machine.",
        "SubSteps": [
          {
            "Label": "1.1",
            "Description": "Unhook the storage hook from the handle bar. The handle bar should automatically lift once the hook is released.",
            "VirtualObjects": []
          },
          {
            "Label": "1.2",
            "Description": "Make sure all the pink pegs, from number 1 to 12 are pushed in.",
            "VirtualObjects": []
          },
          ...
        ]
      },
      ...
    ]
  },
  "RuntimeSystemUtterances": [
    {
      "StartTime": 638763760901582593,
      "EndTime": 638763760951502593,
      "Contents": "Hi! This is Sigma, your mixed-reality task assistant.",
      "PartialContents": [
        {
          "Words": "Hi!",
          "Time": 638763760921268843
        },
        {
          "Words": "Hi! This",
          "Time": 638763760923076968
        },
        {
          "Words": "Hi! This is",
          "Time": 638763760924483218
        },
        {
          "Words": "Hi! This is Sigma,",
          "Time": 638763760928902593
        },
        {
          "Words": "Hi! This is Sigma, your",
          "Time": 638763760932317593
        },
        {
          "Words": "Hi! This is Sigma, your mixed-reality",
          "Time": 638763760939348843
        },
        {
          "Words": "Hi! This is Sigma, your mixed-reality task",
          "Time": 638763760942763843
        },
        {
          "Words": "Hi! This is Sigma, your mixed-reality task assistant.",
          "Time": 638763760951201343
        }
      ]
    },
    {
      "StartTime": 638763760953793317,
      "EndTime": 638763760994753317,
      "Contents": "Today I'm here to help you make a notebook using a binding machine.",
      "PartialContents": [ ... ]
    },
    ...
  ],
  "RuntimeUserUtterances": [ ... ]
  "ManuallyTranscribedUserUtterances": [ ... ]
  "StepExecutionData": [
    {
      "StartTime": 638763761189284448,
      "EndTime": 638763761870436528,
      "StepIndex": 0
    },
    ...
  ],
  "SubStepExecutionData": [
    {
      "StartTime": 638763761221913104,
      "EndTime": 638763761531655316,
      "StepIndex": 0,
      "SubStepIndex": 0
    },
    ...
  ]
}
```

The session metadata includes the session name, the session start and end times expressed in [ticks](#timing), the task name and a short version of the task name, the participant id, the participant task order (e.g. 1 if this is the first task the participant performed, 2 if it's the second, etc.), the task completion status (can be `Correctly Completed`, `Incorrectly Completed`, `Abandoned` or `System Failure`), and the dataset slice this session belongs in (i.e., `A`, `B` or `C`).

The task recipe includes the task name and the set of steps and corresponding substeps. 

Information is available about the production of both system and user utterances, under the attributes `RuntimeSystemUtterances` for the system, and `RuntimeUserUtterances` (for the user utterances detected and recognized by the system at runtime) and `ManuallyTranscribedUserUtterances` (for the manual transcriptions of the actual utterances spoken by the user at runtime). Each of these attributes contain a list of utterances, where for each utterance the start and end time as well as the contents are captured. Additionally, a `PartialContents` field provides information about the incremental production of these utterances, including the word-level timings.

Finally two other attributes: `StepExecutionData` and `SubStepExecutionData` capture the timings (start and end) for each of the high level steps and substeps, as they are executed by the user.


<a name="user_interface_state"></a>
### `user_interface_state` directory

The `user_interface_state` directory contains a file called __{`session_name`}.user_interface_state.json__, where `session_name` is the name of the session. The file stores information about the positioning of the `Sigma` virtual user interface (dialog history bubbles and task panel) in a `.json` format. The file contains a list of datapoints, each containing a [timestamp](#timing) for the datapoint, and a hierarchical description of the 3D rectangles containing the dialog history bubbles and task panel user interface elements.


<a name="timing"></a>

## Timing information

Timing information (e.g. the various date and time fields) in the dataset is represented in [.NET ticks](https://learn.microsoft.com/en-us/dotnet/api/system.datetime.ticks?view=net-9.0). A single tick represents one hundred nanoseconds or one ten-millionth of a second. There are 10,000 ticks in a millisecond and 10 million ticks in a second. The ticks value in the data captures the number of 100-nanosecond intervals that have elapsed since 12:00:00 midnight, January 1, 0001 in the Coordinated Universal Time. 

A simple function for converting ticks to python datetime objects is:

```python
import datetime

def ticks_to_datetime(ticks):
    # .NET ticks start from 0001-01-01 00:00:00
    # 1 tick = 100 nanoseconds = 0.0000001 seconds
    # There are 621355968000000000 ticks between 0001-01-01 and 1970-01-01 (Unix epoch)
    return datetime.datetime(1, 1, 1) + datetime.timedelta(microseconds=ticks // 10)
```

Note that python datetime objects have less temporal resolution than .NET ticks, the lowest unit being 1 microsecond in python, vs 100 nanoseconds in the .NET ticks. Hence the `// 10` in the code above.