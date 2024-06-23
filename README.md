# 计算机视觉-项目报告


## **一、项目简介**

项目名称：High Dynamic Range Imaging

成员名称：吴俊杰、欧如根

项目视频链接： 

 ## **二、绪论**

 高动态范围（High Dynamic Range，简称HDR）成像是一种技术，旨在捕捉、处理和展示比传统数字成像技术更宽广的亮度和色彩范围的图像。在自然界中，光线强度的变化幅度非常大，从直射的日光到深邃的阴影，这个范围远远超过了大多数相机传感器和显示设备的标准动态范围。HDR成像的目标就是尽可能接近人眼所能看到的这种广泛的亮度差异，从而创造出更加真实、生动和细节丰富的图像。

HDR成像的过程通常包括以下几个步骤：

多曝光拍摄：拍摄同一场景的多张照片，每张照片采用不同的曝光设置。这样可以从过度曝光的照片中获取暗部细节，从欠曝光的照片中获得亮部细节，以及从正常曝光的照片中获取中间色调信息。

图像对齐：由于拍摄多张照片时可能会有微小的相机移动，需要将这些照片精确对齐，确保在合并时不会出现模糊或重影。

图像合并：将这些不同曝光的照片合并成一张32位浮点图像，这样就能包含从极暗到极亮的所有亮度信息，形成一张高动态范围图像（HDR图像）。

色调映射：由于大多数显示设备（如电脑屏幕、电视机）只能显示有限的动态范围（通常是标准动态范围，SDR），因此需要通过色调映射将HDR图像转换为可在这些设备上显示的形式，同时尽量保持原图像的视觉效果，比如亮度、对比度和色彩饱和度。

在色调映射中使用了三种算法进行对比：Drago Tonemap、Reinhard Tonemap、Mantiuk Tonemap.

## **三、相关工作**

## **1、文献**

Huo Y ,Gan J ,Jiang W .Multi-exposure high dynamic range imaging based on LSGAN[J].Displays,2024,83102707-.

Siqi H ,Hankun L ,Yonghong Y , et al.Calibrating lighting simulation with panoramic high dynamic range imaging[J].Journal of Building Performance Simulation,2024,17(1):74-93.

Junbao H ,Lingfeng W ,Na L .High dynamic range imaging by a pseudo exposure fusion method based on artificial remapping[J].Optik,2022,260

Mohamed A ,Osman H ,Falah A , et al.High Dynamic Range Photocurrent Sensory Circuit with a Multi-Transistor Background Light Cancellation Loop for Photoplethysmography Sensing[J].Electronics,2021,10(22):2769-2769.

Michael K ,Athanasios T .Non-Intrusive Luminance Mapping via High Dynamic Range Imaging and 3-D Reconstruction[J].Journal of Physics: Conference Series,2021,2042(1):

Qingsen Y ,Dong G ,Qinfeng J S , et al.High dynamic range imaging via gradient-aware context aggregation network[J].Pattern Recognition,2022,122

Jiang Q ,Huang Y ,Liu S , et al.A Novel Attention-guided Network for Deep High Dynamic Range Imaging[C]//西交利物浦大学(Xi'an Jiaotong-Liverpool University), 东京理科大学(Tokyo University of Science),思科网络学院(Cisco Networking Academy).Proceedings of 2021 3rd International Conference on Advances in Computer Technology, Information Science and Communications (CTISC2021).College of Computer Science and Technology Chongqing University of Posts and Telecommunications;School of Software Engineering Chongqing University of Posts and Telecommunications;,2021:6.DOI:10.26914/c.cnkihy.2021.018301.

Keiichiro T ,Miu T ,Takuro I .Adaptive dynamic range shift (ADRIFT) quantitative phase imaging[J].Light: Science & Applications,2021,10(1):

## **2.前沿进展**

高动态范围成像（High Dynamic Range Imaging, HDR）领域持续发展，近年来的最前沿进展主要集中在以下几个方面：
深度学习与人工智能应用：随着机器学习和深度学习技术的飞速发展，HDR成像也开始融入这些先进技术。研究人员开发了多种基于深度神经网络的算法，用于自动对齐、图像融合、色调映射等过程，提高了效率和效果。例如，使用多尺度密集网络（Multi-scale Dense Networks）和深度高动态范围成像技术（Deep High Dynamic Range Imaging）处理动态场景，能够更准确地对齐图像并减少人工痕迹，生成更自然的HDR图像。

实时HDR处理：在视频监控、游戏、直播等领域，实时HDR处理成为一个重要研究方向。这要求算法不仅能够高效处理数据，还要在计算资源有限的情况下实现高质量的HDR效果。为此，研究人员正努力开发低延迟、高性能的算法，以满足实时应用的需求。

高动态范围显示技术的进步：随着HDR显示器的普及，如何优化HDR内容的制作以匹配这些新型显示设备成为新的研究点。这包括开发新的色调映射算法，以充分利用HDR显示的宽广动态范围，同时保持视觉舒适性和真实感。

HDR标准与兼容性：为了推动HDR技术的标准化，行业组织和企业正在制定统一的标准和规范，确保不同设备和平台间HDR内容的互操作性。这包括色彩空间、元数据处理、传输协议等方面的标准制定。

动态场景HDR成像：针对运动物体的HDR成像一直是技术难点。最新的研究聚焦于如何有效处理动态场景中的运动模糊、鬼影等问题，利用光流估计、时空一致性优化等技术，改善动态HDR图像的质量。

扩展应用场景：HDR技术不再局限于传统的摄影和影视制作，它正被应用于虚拟现实（VR）、增强现实（AR）、医疗成像、遥感技术等多种领域，推动这些领域的图像质量和用户体验提升。

## **四、方法具体细节描述**

项目实现分为以下阶段：运行环境配置、读取图像和曝光时间、图像对齐、恢复相机响应功能、合并图像、色调映射。

## **1.运行环境配置**

配置环境 python与opencv导入包
import cv2
import numpy as np

## **2.读取图像和曝光时间**

手动输入图像，曝光时间以及图像个数。
def readImagesAndTimes():
 # 图像文件名列表
  times = np.array([ 1/30.0, 0.25, 2.5, 15.0 ], dtype=np.float32)
   
 # 图像文件名列表
  filenames = ["img_0.033.jpg", "img_0.25.jpg", "img_2.5.jpg", "img_15.jpg"]
  images = []
  for filename in filenames:
    im = cv2.imread(filename)
    images.append(im)
   
  return images, times

readImagesAndTimes()函数的作用是从给定的文件名列表中读取一系列图像文件，并记录它们对应的曝光时间，然后返回这两个信息集合。首先曝光时间列表，函数使用NumPy库创建了一个名为times的数组，该数组存储了四个不同的曝光时间。曝光时间从1/30秒到15秒不等，这样的设计是为了覆盖从较暗到较亮场景的广泛光照条件。接着图像文件名列表，定义了一个字符串列表filenames，其中包含了待读取图像文件的名称。每个文件名都暗示了其对应的曝光时间，尽管这里的命名与实际曝光时间不完全对应。读取并收集图像，通过一个循环遍历filenames列表中的每个文件名，使用OpenCV库的cv2.imread()函数逐个读取图像文件，并将读取到的图像对象追加到images列表中。最后返回结果，函数返回两个列表：images包含所有读取到的图像数据，而times则是对应的曝光时间数组。这两个输出可以进一步用于高动态范围（HDR）图像处理，比如图像对齐、HDR合成及色调映射等操作。


## **3.图像对齐**

由于拍摄多张照片时可能会有微小的相机移动，需要将这些照片精确对齐，确保在合并时不会出现模糊或重影。

 # 对齐输入图像
alignMTB = cv2.createAlignMTB()
alignMTB.process(images, images)

 先创建了一个AlignMTB对象，这是OpenCV中用于图像对齐的类，用于HDR图像预处理。通过alignMTB.process(images, images) 对输入的图像序列进行对齐处理。

## **4.恢复相机响应功能**

典型相机的响应与场景亮度不是线性的，但如果我们知道每张图像的曝光时间，可以从图像中估算CRF。

 # 获取摄像头响应功能
calibrateDebevec = cv2.createCalibrateDebevec()
responseDebevec = calibrateDebevec.process(images, times)


 创建了一个用于相机响应函数估计的对象。Debevec方法是一种基于全局优化的算法，常用于从多幅不同曝光时间拍摄的图像中估计相机的响应曲线。估计响应函数: process() 方法接收两组参数：一是包含多张不同曝光图像的列表images，二是对应的曝光时间列表times。它运用Debevec算法处理这些图像和时间信息，输出的结果responseDebevec即为估计得到的相机响应函数（CRF）。

## **5.合并图像**

将这些不同曝光的照片合并成一张32位浮点图像，这样就能包含从极暗到极亮的所有亮度信息，形成一张高动态范围图像（HDR图像）。

 # 将图像合并为HDR线性图像
mergeDebevec = cv2.createMergeDebevec()
hdrDebevec = mergeDebevec.process(images, times, responseDebevec)
 # 保存HDR图像。
cv2.imwrite("hdrDebevec.hdr", hdrDebevec)

在这里，cv2.createMergeDebevec() 创建了一个合并图像的实例，它基于Debevec提出的算法。通过process()方法，传入之前读取和对齐的图像序列images、对应的曝光时间列表times，以及计算出的相机响应函数responseDebevec，来生成一个高动态范围（HDR）图像hdrDebevec。这个HDR图像能够捕捉到比普通图像更广泛的亮度信息，从非常暗的阴影到非常亮的高光部分。最后将生成的HDR图像保存为一个文件，文件名为"hdrDebevec.hdr"。由于普通的图像格式（如JPEG或PNG）无法存储HDR信息，因此必须使用支持HDR的格式，如 Radiance HDR (.hdr) 格式来保存图像。这样，就可以在支持HDR的查看器或进一步的图像处理软件中打开和编辑这个HDR图像了

## **6.色调映射**

由于大多数显示设备（如电脑屏幕、电视机）只能显示有限的动态范围（通常是标准动态范围，SDR），因此需要通过色调映射将HDR图像转换为可在这些设备上显示的形式，同时尽量保持原图像的视觉效果，比如亮度、对比度和色彩饱和度。通过三种算法进行色调映射Drago Tonemap、Reinhard Tonemap、Mantiuk Tonemap。

Drago Tonemap的参数
createTonemapDrago
 
(
 
float   gamma = 1.0f,
 
float   saturation = 1.0f,
 
float   bias = 0.85f
 
)
Reinhard Tonemap的参数
createTonemapReinhard
 
(
 
float   gamma = 1.0f,
 
float   intensity = 0.0f,
 
float   light_adapt = 1.0f,
 
float   color_adapt = 0.0f
 
)
Mantiuk Tonemap的参数
createTonemapMantiuk
 
(  
 
float   gamma = 1.0f,
 
float   scale = 0.7f,
 
float   saturation = 1.0f
 
)
 # 使用Drago方法获得24位彩色图像的色调图
  print("Tonemaping using Drago's method ... ")
  tonemapDrago = cv2.createTonemapDrago(1.0, 0.7)
  ldrDrago = tonemapDrago.process(hdrDebevec)
  ldrDrago = 3 * ldrDrago
  cv2.imwrite("ldr-Drago.jpg", ldrDrago * 255)
  print("saved ldr-Drago.jpg")
 
  # 使用Reinhard方法获得24位彩色图像的色调图
  print("Tonemaping using Reinhard's method ... ")
  tonemapReinhard = cv2.createTonemapReinhard(1.5, 0,0,0)
  ldrReinhard = tonemapReinhard.process(hdrDebevec)
  cv2.imwrite("ldr-Reinhard.jpg", ldrReinhard * 255)
  print("saved ldr-Reinhard.jpg")
  
  # 使用Mantiuk方法获得24位彩色图像的色调图
  print("Tonemaping using Mantiuk's method ... ")
  tonemapMantiuk = cv2.createTonemapMantiuk(2.2,0.85, 1.2)
  ldrMantiuk = tonemapMantiuk.process(hdrDebevec)
  ldrMantiuk = 3 * ldrMantiuk
  cv2.imwrite("ldr-Mantiuk.jpg", ldrMantiuk * 255)
  print("saved ldr-Mantiuk.jpg")

## **五、结果**

三种不同算法色调函数对应结果图
![img](ldr-Drago.jpg)
![img](ldr-Mantiuk.jpg)
![img](ldr-Reinhard.jpg)

最后可以发现，Drago Tonemap能够有效增强图像的局部对比度，
Mantiuk Tonemap在保留图像细节的同时增强色彩饱和度，
Reinhard Tonemap产生的色调映射图像色彩自然，整体亮度分布均匀。

## **六、总结与讨论**

通过努力，项目预期目标基本完成，我们深入探讨了高动态范围成像（HDR）处理的关键技术和步骤，从图像对齐、相机响应函数（CRF）的估计，到HDR图像的合并，以及最后的色调映射处理。

1.技术选择的灵活性与局限性：虽然多种技术和算法提供了处理HDR图像的手段，但每种方法都有其优势和局限性，需根据实际需求和预期效果权衡选择。

2.实时与高质量处理的平衡：实时HDR处理在视频和游戏应用中日益重要，但如何在保持高质量的同时实现低延迟是一大挑战。

3.跨平台兼容性与标准：随着HDR显示技术的发展，确保HDR内容能在不同设备上一致显示，需要遵循相关标准和最佳实践。

## **七、个人贡献说明**

​	欧如根：负责论文文献的阅读，相关资料查询；50%

​	吴俊杰：负责图像的处理、合并、色调映射；50%

​	其实考虑到实际情况，最终分工可能并不是像上述那样准确，但是我们的主要分工大概如此，这样分配的主要原因是发挥小组成员已有基础和长处。


## **八、视频链接**
  https://www.bilibili.com/video/BV1Ns3geoEP5/