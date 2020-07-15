---
title: A basis for 2D to 3D topology transfer
authors: Anuj Som
category: AI For Everyone Projects - Spring 2020
order: 6
---

Anuj Som

Area of research: Computer graphics/simulation/VR development

_Motivations and background_

The creation of 3D spaces is a time-consuming and skill-intensive process. Many game companies expend a large budget on level designers capable of furnishing environments to fit the style of the game, which takes a long time and is difficult to prototype easily. Therefore, I envision creating a system with the use of deep neural network architecture that will be able to read natural landscape features from an image and convert it into a 3D voxel space. The first component of this system is designed below.

This process requires intuition on many levels. For one, it requires a way to learn and associate real-world features to video game features, or vice versa, which is large step to attempt initially. One feasible idea to start is to build off an existing method such as Semantic Image Synthesis with Spatially-Adaptive Normalization (SPADE) which is able to generate realistic 2D landscapes from a collection of segmentation maps. Nvidia&#39;s GauGAN ([http://nvidia-research-mingyuliu.com/gaugan/](http://nvidia-research-mingyuliu.com/gaugan/)), which provides an interactive demo built off SPADE, allows a translation from a realistic space to a segmentation space. This idea can theoretically expand to create an association can between a segmentation space and a 3D voxel space. Thus, one goal of this project is to learn an association between a 3D space and a 2D segmentation map.

Another goal of this project, apart from its viability, is whether video games can be leveraged to provide training datasets or create artificial environments from massive amounts of training data can be generated. This project will attempt to gain insight of this method through the use of Minecraft to simulate realistic terrain generation.

Through the success of this project, game players would be enabled to become game creators by making terrain generation much more accessible. Researchers could also use this method as a simulated environment for a wide range of tasks. As there is not a tremendous amount of research which looks at utilizing video games for the generation of data, this is a project which hopes to generate interest in using video games as a tool for data acquisition.

_Dataset_

As one goal of this is to test the efficacy of data generated from video game content, the data collected was of screenshots of Minecraft terrain at a full 32-chunk render distance with as much resolution as possible. The terrain ranged from mountainous to beachy to forested, with particular focus on the number of distinct features or topographical differences. The terrain generated utilized the TerraForged mod ([https://www.curseforge.com/minecraft/mc-mods/terraforged](https://www.curseforge.com/minecraft/mc-mods/terraforged)

) for Minecraft version 1.15.2. Features of this mod allowed the modification of noise (such as simplex perlin), biome size, lacunarity, and so on, making it (along with the Minecraft terrain generation algorithm) an effective tool at generating infinitely different landscapes.

Currently the dataset comprises of 57 high-resolution photos, as well as every tenth frame taken from video shot in Minecraft, totaling over 500 photos. One limitation of taking frames from a video is that it places more emphasis on a certain biome type over another, and may cause problems with post-processing bias. However, this problem can be solved over time with greater amounts of more varied data.

Each screenshot has a resolution of 1920 x 1080 pixels, with full RGB color, making it a highly dense dataset. This factor made it nearly impossible to actually train a model with a CPU, one large limitation during the project due to unforeseen circumstances (namely the COVID-19 pandemic and losing the Duke GPU computing cloud resource).

In order to label this dataset accurately, a few different methods have been thought of. One was incorporating the Minecraft texture pack as distinguishing filters during convolution steps. However one limitation of this is Minecraft&#39;s biome color correction (for grass) as well as possibly abstracting large features (mountains vs hills, rivers vs lakes, etc.). Another approach that focuses more on the topology is by using Holistically-Nested Edge Detection (HED) ([https://arxiv.org/pdf/1504.06375.pdf](https://arxiv.org/pdf/1504.06375.pdf)) (as opposed to the Canny edge detection algorithm) to detect feature boundaries and generate segmentation maps that can also potentially carry topological information.

_Data Preprocessing_

Data that contained too large a portion of sky or included the sun/moon (which would likely create artifacts later when associating with photorealistic images) were removed. Data that were taken when not enough of the scene was rendered (i.e. distinct chunk boundaries, see-through ground) were discarded and the higher-quality frames were used instead.

During training, the dataset could feasibly be augmented through reflections, rotations, or transformations. However, due to how easy it is to find unique terrain in Minecraft, it is unnecessary to perform this step. Another approach that may be better is cropping 500 x 500 different areas of the captured images which can alleviate computing cost during each step as well as greatly increasing data.

The data itself is normalized after each convolutional step, a novel architecture as specified in the SPADE paper. This project will eventually attempt to build largely on this methodology, after extracting a basic feature boundaries with HED (specified in this project).

In future methodologies, I recognize the potential that creating mods for Minecraft has in toggling day/night cycles, teleporting to landmasses, and potentially completely automating the data-acquisition process. This would only require someone to clean up the data afterwards, and is worth consideration in future methods that rely on gaining data from video games.

_Machine Learning Methodology_

Focusing on extracting feature boundaries, with specific focus on preserving topographic features unique to the Minecraft Game, the Holistically-Nested Edge Detection model was ultimately chosen. Because the task at hand is essentially a classification task of different regions of an image, it is useful to use a convolutional neural network (CNN) which is capable of scanning an image with ever-increasing detailed filters. However, the HED network is a modified convolutional neural network which weights outputs from each convolutional step by fusing it with the ground truth. This supervision step after each convolution allows greater feature transfer to the final layer, and reduces cluttering caused by unimportant features. The ground truth of an image can be created from utilizing Canny edge detection and adjusting the contrast settings of the image.

The capabilities of HED is preferred over strictly using Canny edge detection due to the better preservation of feature boundaries and the capability to recognize context through variable thresholds as opposed to fixed ones. This approach will hopefully allow, when combined with a CNN that recognizes block types and biomes (dirt, mud, mountain, water, river, snow, etc.) will allow a comprehensive image segmentation map. HED is useful in also preserving the &#39;blockiness&#39; characteristic to Minecraft which will hopefully be learned by the net.

Unfortunately, the training of the model was impossible due to the unforeseeable circumstances. One noticeable limitation was the length of training on a CPU with the full resolution (unbearably slow), and using an autoencoder was considered to condense the information before training. This may be viable for producing the segmentation map, but it is unknown if it will ultimately produce artifacts in the data. If this method was used, it is likely that model parameters would be chosen as a result to best use the encoding step. However, as it stands, the model would have copied the architecture used in the HED paper, with modifications as necessary to save computation time and power. The paper used five convolutional layers, with strides 1, 2, 4, 8, and 16.

_Results_

Although my network was ultimately unable to be trained, the project was definitively successful in the aspect that I learned a lot behind network architecture and novel approaches which increase efficiency of existing systems, specifically regarding the changes made to HED and SPADE to increase their success and make them robust systems from which we can learn.

One methodology that I particularly believe will allow a large degree of flexibility in the future is the concept of utilizing basic feature segmentation maps as a bridge between high-motif styles (namely Minecraft and photorealistic styles). I believe much more work will be needed in order to learn 3D terrain from the 2D Minecraft photos, however this can definitely be achieved through modding and understanding of 3D voxel space. If this idea is eventually fully implemented, I can see a future where pictures are turned into segmentation maps then translated into a Minecraft, or GTA, or Skyrim map file that can be exported and experimented with.

_Conclusion_

With respect to the long-term aims, this approach seems promising as it will allow us to bridge the gap between 2D and 3D, potentially allowing more access to VR/AR technologies of which I am personally fond of and wish to academically contribute to in the future. While its current implementation does not push the state-of-the-art boundaries, it holds potential to become an essential tool in the future for content creators and researchers alike.

From what was able to be tested, the system holds potential to be satisfactory, but this project ultimately was unsuccessful due to the unforeseen circumstances, resource limitations, and/or unoptimized architecture. Under better conditions, I sincerely hope to continue this work and make it work out.

One unexpected pitfall, of course, was the COVID-19 crisis, but another aspect that took a large amount of my time was the manipulation of .png or .jpg and RGB or RGBA and the myriads of different forms these files took and getting them to be recognized by the software I wrote. I believe that with a better understanding of Python, it would have been easier to manage the photos and get them into tensor formats easier. Another pitfall, which was similar to this but ever increasingly difficult, was reading the frame data of the Quicktime movie and saving every 10th frame. On top of that, getting the correct setting for them after I had saved the frame was incredibly difficult.

The area that needs the most improvement was my comprehension of computer science papers, especially the highly technical ones such as the SPADE and HED papers. While incredibly interesting architectures, many of the concepts that were introduced took a long time to digest. Another area that I wish to improve in is my Python literacy, which would have saved a lot of time while wrestling the pitfalls. I wish to also eventually learn how to code Minecraft mods to automatically gather terrain pictures and maybe even terrain topographic data.

In order to achieve the desired system, all of these goals must be reached. I believe that with proper computational resources (namely a GPU and maybe a team member), it will be possible to use an autoencoder step, perform the convolutions for both the HED boundary edge detections, combine it with a color map identifier and classifier, which will ultimately generate the segmentation map. Then, I can use the SPADE architecture, or existing GauGAN to produce photorealistic images based off the Minecraft scene. By training these networks repeatedly, I hope to eventually work the association backwards and produce a Minecraft scene from a photorealistic picture. Finally, a network would have to be trained to learn 3D Minecraft data from the 2D Minecraft photos. I envision there will be much difficulty in developing a scene from the generated Minecraft scenes based on a photorealistic image, so I must think of a way to preserve the &quot;blockiness&quot; in the association between the data and segmentation maps in this early stage of the project. The method I used to do this was using HED, with its capabilities to learn threshold values and identify and preserve edges, as attempted in this paper.

_References_:

&quot;Canny Edge Detection.&quot; _OpenCV_, docs.opencv.org/trunk/da/d22/tutorial\_py\_canny.html.

Chen, Liang-Chieh., Papandreou, George., &quot;DeepLab: Semantic Image Segmentation with Deep Convolutional Nets, Atrous Convolution, and Fully Connected CRFs&quot;, 2017, https://arxiv.org/pdf/1606.00915.pdf

Park, Taesung., Liu, Ming-Yu., Wang, Ting-Chun. Zhu, Jun-Yan., &quot;Semantic Image Synthesis with Spatially-Adaptive Normalization&quot;, _UC Berkely, NVIDIA, MIT CSAIL_, 2019, https://arxiv.org/pdf/1903.07291.pdf

Wang, Ting-Chun., Liu, Ming-Yu., Zhu, Jun-Yan., Tao, Andrew., Kautz, Jan., Catanzaro, Bryan., &quot;High-Resolution Image Synthesis and Semantic Manipulation with Conditional GANs&quot;, _NVIDIA, UC Berkely_, 2018, https://arxiv.org/pdf/1711.11585.pdf

Xie, Saining. Tu, Zhuowen, &quot;Holistically-Nested Edge Detection&quot;, Proceedings of IEEE International Conference on Computer Vision, 2015, https://arxiv.org/pdf/1504.06375.pdf