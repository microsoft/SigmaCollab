# SigmaCollab: A Dataset for Situated Collaboration

__`SigmaCollab`__ is a dataset that enables research on human-AI physically situated collaboration. The dataset consists of a set of 85 sessions in which untrained participants were guided by a mixed-reality assistive AI agent in performing procedural tasks in the physical world, plus an additional 8 sessions in which the system guided an expert in performing the same tasks.

![`SigmaCollab` data](InteractionSample.png)

The dataset, described in detail in [this arxiv paper](to-fill-in), was collected with an open-source mixed-reality AI application called [Sigma](https://github.com/microsoft/psi/blob/master/Applications/Sigma/Readme.md) (itself described in [this arxiv paper](https://arxiv.org/abs/2405.13035) and in an [IEEE VR extended abstract](https://ieeexplore.ieee.org/abstract/document/10536320)). The _application-driven_ and _interactive_ nature of the __`SigmaCollab`__ dataset bring to the fore novel research challenges for human-AI collaboration, and provide more realistic testing grounds for various AI models operating in this space. Additionally, the [Sigma](https://github.com/microsoft/psi/blob/master/Applications/Sigma/Readme.md) system is open-source, and you can download and run it yourself to collect your own / additional data.

## Dataset contents

__`SigmaCollab`__ includes a set of rich, multimodal data streams: the participant and system audio, egocentric camera views from the head-mounted device, depth maps, head, hand and gaze tracking information, as well as additional annotations performed post-hoc. The raw set of data streams included is summarized in the table below:

| Stream                          | Representation                                                                                                    | Avg. Frame Rate |
|----------------------------------|------------------------------------------------------------------------------------------------------------------|:---------------------:|
| RGB Camera View                  | 896 × 504 pixels @ 24bpp, with camera pose and intrinsics                                                         | 14.91 Hz              |
| Depth Camera View                | 320 × 288 pixels @ 16bpp, with camera pose and intrinsics                                                        | 4.98 Hz               |
| Left Front Grayscale Camera View | 640 × 480 pixels @ 8bpp, with camera pose and intrinsics                                                         | 13.64 Hz              |
| Right Front Grayscale Camera View| 640 × 480 pixels @ 8bpp, with camera pose and intrinsics                                                         | 13.64 Hz              |
| Head Pose + Eye Gaze             | tuple of head pose matrix (4 × 4) and eye gaze ray (3 × 1 origin position vector and 3 × 1 direction vector)     | 28.37 Hz              |
| Hands Pose                       | pose matrices (4 × 4) for each of the 26 joints in the left and right hand                                       | 20.01 Hz              |
| Audio                            | 1-channel, 32-bit floating-point PCM                                                                             | 16.00 kHz             |

<br>

__`SigmaCollab`__ also includes manual segmentation and transcripts for the user utterances, word-level timings for both user and system utterances, task success annotations, as well as post-processed gaze information (e.g., projection of gaze point in the various camera images). For more details regarding the dataset contents, structure, and data formats, please see the [Dataset Structure](DatasetStructure.md) documentation page.

<a name="download"></a>
## Download

To download the dataset, start by cloning this repo: 

```bash
git clone https://github.com/microsoft/SigmaCollab
cd SigmaCollab
```

And then use the following `wget` command to download the entire dataset (~100GB):

```bash
wget -i download/all_sessions
```

You can also download only portions of the dataset, corresponding to each of the modalities / directories described in [Dataset Structure](DatasetStructure.md), e.g.:

```bash
wget -i download/all_sessions.image             # downloads images (depth, color, leftfrontgrayscale, rightfrontgrayscale) for all sessions
wget -i download/participant_sessions.image          # downloads images (depth, color, leftfrontgrayscale, rightfrontgrayscale) only for the participant sessions
wget -i download/all_sessions.image.color       # downloads the color images for all sessions
wget -i download/expert_sessions.audio     # downloads the audio for the 8 expert demonstration sessions
```

In the commands above, you can use the `all_sessions`, `participant_sessions`, and `expert_sessions` monikers to specify which sessions to download, followed by the modaly names as described in [Dataset Structure](DatasetStructure.md).
The commands will download a set of corresponding .tag.gz files, which you can decompress into a data subdirectory as follows:

```bash
mkdir data
for f in *.tar.gz; do tar -xzf "$f" -C data; done
```


## Citation

If you use this dataset in your research, please cite the following paper:
```
We are in the process of publishing this paper to arxiv, and will place the bibtex here when complete in the next couple of days. Please check again later.
```


## License

The data for the SigmaCollab dataset is made available under the [CDLA-Permissive-2.0](CDLA.txt) license.
The files in this github site are made available under the [MIT License](LICENSE).

## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit [Contributor License Agreements](https://cla.opensource.microsoft.com).

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

## Trademarks

This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft
trademarks or logos is subject to and must follow
[Microsoft's Trademark & Brand Guidelines](https://www.microsoft.com/legal/intellectualproperty/trademarks/usage/general).
Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship.
Any use of third-party trademarks or logos are subject to those third-party's policies.
