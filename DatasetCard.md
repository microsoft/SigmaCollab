---
license: cdla-permissive-2.0
language:
- en
pretty_name: SigmaCollab
---
# HuggingFace Dataset Card for SigmaCollab

<!-- Provide a quick summary of the dataset. -->
__`SigmaCollab`__ is a dataset that enables research on human-AI physically situated collaboration. The dataset consists of a set of 85 sessions in which untrained participants were guided by a mixed-reality assistive AI agent in performing procedural tasks in the physical world. 

## Dataset Details

### Dataset Description

<!-- Provide a longer summary of what this dataset is. -->

__`SigmaCollab`__, described in detail in [this arxiv paper](to-fill-in), was collected with an open-source mixed-reality AI application called [Sigma](https://github.com/microsoft/psi/blob/master/Applications/Sigma/Readme.md) (itself described in [this arxiv paper](https://arxiv.org/abs/2405.13035) and in an [IEEE VR extended abstract](https://ieeexplore.ieee.org/abstract/document/10536320)). The _application-driven_ and _interactive_ nature of the __`SigmaCollab`__ dataset bring to the fore novel research challenges for human-AI collaboration, and provide more realistic testing grounds for various AI models operating in this space. Additionally, the [Sigma](https://github.com/microsoft/psi/blob/master/Applications/Sigma/Readme.md) system is open-source, and you can download and run it yourself to collect your own / additional data.

__`SigmaCollab`__ includes a set of rich, multimodal data streams: the participant and system audio, egocentric camera views from the head-mounted device, depth maps, head, hand and gaze tracking information, as well as additional annotations performed post-hoc. The raw set of data streams included is summarized in the table below:

| Stream                          | Representation                                                                                                    | Avg. Frame Rate |
|----------------------------------|------------------------------------------------------------------------------------------------------------------|:---------------------:|
| RGB Camera View                  | 896 × 504 pixels @ 24bpp, with camera pose and intrinsics                                                         | 14.91 Hz              |
| Depth Camera View                | 320 × 288 pixels @ 16bpp, with camera pose and intrinsics                                                        | 4.99 Hz               |
| Left Front Grayscale Camera View | 640 × 480 pixels @ 8bpp, with camera pose and intrinsics                                                         | 13.64 Hz              |
| Right Front Grayscale Camera View| 640 × 480 pixels @ 8bpp, with camera pose and intrinsics                                                         | 13.65 Hz              |
| Head Pose + Eye Gaze             | tuple of head pose matrix (4 × 4) and eye gaze ray (3 × 1 origin position vector and 3 × 1 direction vector)     | 28.37 Hz              |
| Hands Pose                       | pose matrices (4 × 4) for each of the 26 joints in the left and right hand                                       | 20.01 Hz              |
| Audio                            | 1-channel, 32-bit floating-point PCM                                                                             | 16.00 kHz             |

Additionally, __`SigmaCollab`__ includes manual segmentation and transcripts for the user utterances, word-level timings for both user and system utterances, task success annotations, as well as post-processed gaze information (e.g., projection of gaze point in the various camera images). For more details regarding the dataset contents, structure, and data formats, please see the [Dataset Structure](https://github.com/microsoft/SigmaCollab/blob/master/DatasetStructure.md) documentation page.


- **Curated by:** [More Information Needed]
- **Language(s) (NLP):** English
- **License:** [CDLA-Permissive-2.0](https://github.com/microsoft/SigmaCollab/blob/master/CDLA.md)

### Dataset Sources

- **Repository:** [https://github.com/microsoft/SigmaCollab](https://github.com/microsoft/SigmaCollab)
- **Paper:** [SigmaCollab: An Application-Driven Dataset for Physically Situated Collaboration]()

## Uses

<!-- Address questions around how the dataset is intended to be used. -->
__`SigmaCollab`__ aims to catalyze rigorous, application-grounded study of fluid human–AI collaboration and to close the gap between lab benchmarks and real-world performance.

## Dataset Structure

<!-- This section provides a description of the dataset fields, and additional information about the dataset structure such as criteria used to create the splits, relationships between data points, etc. -->

Details regarding the dataset contents, structure, and data formats are available in this [documentation page](https://github.com/microsoft/SigmaCollab/blob/master/DatasetStructure.md).

## Dataset Creation

### Curation Rationale

<!-- Motivation for the creation of this dataset. -->

While significant progress has been made over the past decade towards building computing systems that interact with people in the physical world, a lot of the existing datasets focus on computer vision or language processing challenges. However, in addition to understanding the environment, objects, and actions, creating seamless situated collaborations raises additional _interaction_- and _collaboration_-related challenges. In these areas, progress has been slower. 

__`SigmaCollab`__ was developed to foster and enable more research on such challenges. In future work, we plan to construct and publish a set of benchmarks in this space based on this dataset.

### Source Data

<!-- This section describes the source data (e.g. news text and headlines, social media posts, translated sentences, ...). -->

__`SigmaCollab`__ was constructed via a data collection experiment in which participants interacted with the open-source [Sigma](https://github.com/microsoft/psi/blob/master/Applications/Sigma/Readme.md) system to perform a set of procedural tasks. The data experiment was conducted in a lab at Microsoft Research and was approved by the Microsoft Research Institutional Review Board.

#### Data Collection and Processing

<!-- This section describes the data collection and processing process such as data selection criteria, filtering and normalization methods, tools and libraries used, etc. -->


The dataset was collected by having untrained participants interact with a mixed-reality assistive AI application ([Sigma](https://github.com/microsoft/psi/blob/master/Applications/Sigma/Readme.md)) which guided them in real-time in performing certain tasks in the physical world, such as binding a notebook or installing the wheels on a skateboard. 

#### Who are the source data producers?

<!-- This section describes the people or systems who originally created the data. It should also include self-reported demographic or identity information for the source data creators if this information is available. -->

We recruited participants for the study from among the co-workers at our organization, via broadly reaching emails and word-of-mouth. In total 21 participants (12 male and 9 female) engaged in the data collection study and provided permission for public data release. Most participants were in the 46-55 age bracket. While their level of familiarity with AR/VR technologies varied, most participants had already encountered these technologies, even if they were not using them often.

### Annotations
<!-- If the dataset contains annotations which are not part of the initial data collection, use this section to describe them. -->

__`SigmaCollab`__ includes manual segmentation and transcripts for the user utterances, word-level timings for both user and system utterances, task success annotations, as well as post-processed gaze information (e.g., projection of gaze point in the various camera images). For more details regarding the dataset contents, structure, and data formats, please see the [Dataset Structure](https://github.com/microsoft/SigmaCollab/blob/master/DatasetStructure.md) documentation page.

#### Annotation process

<!-- This section describes the annotation process such as annotation tools used in the process, the amount of data annotated, annotation guidelines provided to the annotators, interannotator statistics, annotation validation, etc. -->

[More Information Needed]

#### Who are the annotators?

<!-- This section describes the people or systems who created the annotations. -->

[More Information Needed]

#### Personal and Sensitive Information

<!-- State whether the dataset contains data that might be considered personal, sensitive, or private (e.g., data that reveals addresses, uniquely identifiable names or aliases, racial or ethnic origins, sexual orientations, religious beliefs, political opinions, financial or health data, etc.). If efforts were made to anonymize the data, describe the anonymization process. -->

[More Information Needed]

## Bias, Risks, and Limitations

<!-- This section is meant to convey both technical and sociotechnical limitations. -->

[More Information Needed]

### Recommendations

<!-- This section is meant to convey recommendations with respect to the bias, risk, and technical limitations. -->

Users should be made aware of the risks, biases and limitations of the dataset. More information needed for further recommendations.

## Citation

<!-- If there is a paper or blog post introducing the dataset, the APA and Bibtex information for that should go in this section. -->

**BibTeX:**

[More Information Needed]

## Dataset Card Contact

dbohus@microsoft.com<br>
sandrist@microsoft.com<br>
maiastiber@microsoft.com<br>