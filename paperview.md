[TOC]
#专有名词缩写
AF：atrial fibrillation  房颤
AFL：atrial flutter  房扑
PAB：房早
AT：房速
PVC：室早
VT：室速
VFL：室扑
VF：室颤
#1.Algorithmic Principles of Remote-PPG
###期刊类型：SCI
IEEE TRANSACTIONS ON BIOMEDICAL ENGINEERING, VOL. PP, NO. 99, MONTH 2016
###小木虫论坛链接：
http://muchong.com/bbs/journal.php?jid=3382&view=detail
###摘要：
###总结：
###方法：
#2.基于卷积神经网络的深度学习算法与应用研究
###论文类型：硕士论文
###作者：陈先昌
###摘要：
在LeNet-5网络模型的基础上进行改进，构造了若干各层具有不同神经元个数和层间连接方式的特征抽取滤波器层的卷积神经网络模型，将各个模型应用到光学数字识别问题上，通过这些不同的卷积神经网络模型在实验中学习过程表现出的特性和识别性能分析比较各种模型的优劣。、通过借鉴自适应增强的思想，构建了一个多列卷积神经网络模型，并将其应用在交通标示识别实际应用问题中，将数据进行预处理，训练卷积神经网络，实现卷积神经网络对交通标示的高性能识别。、通过实验最终验证卷积神经网络在手写数字识别和交通标示识别问题上的应用可行性。并与其他现有的分类器进行比较，分析卷积神经网络模型在各种实际应用问题上的性能。
##个人解读：
调整了一个已有（LeNet-5）的模型的参数，增加、减少节点，层数，激活函数，做了一下效果对比。
在之前的基础上构建了25个分类器，再平均25个分类器的结果作为最终结果。
#3.Detecting Atrial Fibrillation and Atrial Flutter in Daily Life Using Photoplethysmography Data(重要论文)
###期刊类型：SCI
IEEE JOURNAL OF BIOMEDICAL AND HEALTH INFORMATICS
###作者：
Linda M. Eerik¨ainen, Student Member, IEEE, Alberto G. Bonomi, Fons Schipper, Lukas R.C. Dekker,
Helma M. de Morree, Rik Vullings, and Ronald M. Aarts, Fellow, IEEE
###摘要：
Photoplethysmography (PPG) enables unobtrusive heart rate monitoring, which can be used in wrist-worn applications. Its potential for detecting atrial fibrillation (AF) has been recently presented. Besides AF, another cardiac arrhythmia increasing stroke risk and requiring treatment is atrial flutter(AFL). Currently, the knowledge about AFL detection with PPG is limited. The objective of our study was to develop a model that classifies AF, AFL, and sinus rhythm with or without premature beats from PPG and acceleration data measured at the wrist in daily life.
###<font color='red'>重要意义：</font>
PPG could indicate presence of AFL, not only AF.
<font color='red' size='6'>首次：PPG信号不但能检测房颤，也能检测房扑。</font>
###作者总结：
In this study, we demonstrated that PPG and acceleration
measurements at the wrist can be used to discriminate between
AF, AFL, and other rhythms in daily life. We showed that
with an AF vs. non-AF model and AF and AFL vs. other
rhythms model that used only information derived from interpulse
intervals, the false detections were for a large part caused
by AFL. The multi-rhythm model included more information
from the wrist measurement, such as features from the PPG
waveform and accelerometer data. This model was not only
able to improve the overall performance of AF detection, but
could also classify AFL with high accuracy. The results of
this study indicate that the PPG signal contains sufficient
information, derived both from the waveform and IPIs, to
accurately classify between AF, AFL, and other rhythms. Thus,
PPG could provide promising means to detect AFL along with
AF.
论证了PPG和**腕带加速器测量值**能用来区分AF,AFL和其他类型的心律律动。
仅用脉搏间隔信息，利用**AF vs 非AF模型**，**AF&AFL vs 其他律动模型**证明了结论，错误检测很大一部分来自AFL。混合律动模型包含了更多的腕带测量信息，比如PPG特征波形和加速器数据。该模型不但能提高AF检测的整体性能，也能高精度的分类AFL。研究结果表明从波形和脉搏间隔PPG信号包含足够多的的信息，可以精确分类AF,AFL,和其他律动。
###方法method：
数据：24小时×40人 同步的ECG,PPG和腕带加速器测量值
预处理和波峰检测：PPG信号降采样从128HZ->64HZ,频率过滤到0.3-5HZ,
pulses通过检测基准点，波谷通过局部最小值检测,计算2个连续基准点的时间差获得脉冲间隔IPIs（inter-pulse intervals）。
IPI时间序列来匹配标注的ECG搏动时间
模型结构：
![](/images/模型1.png)

+ 基于传统IPI变异模式
+ 混合模型
+ 在30S的不重叠的窗口中对PPG,加速剂，IPI时间序列进行分割来计算特征，并基于节奏来标记窗口。ECG的搏动标记作为基准，大多数的搏动为AF时，窗口标记为AF，同理标记AFL。窗口中有SVPB且没有AF&AFL,窗口标记为SVPB，同理标记VPB,其他的标记为正常。标记为伪影的舍弃。
+ 二分类
    1 AF为一类，其他为一类
    2 AF&AFL为一类，然后移除AFL
+ 多分类
    1 AFL为一类，NSR&SVPB&VPB为一类
    2 早搏没有分类，一是例子太少，二是一般不需要治疗
###特征：
![](/images/特征.png)
<font color='red'>pNN40 pNN70是什么？</font>
###特征选择：
+ 二分类
Minimal-Redundancy-Maximal-Relevance (mRMR)最小冗余最大相关法
根据MRMR的特征排序选择1-6个特征，最后根据准确度确定特征

+ 多分类
用随机森林选出特征