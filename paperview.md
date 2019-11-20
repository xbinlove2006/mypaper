```
[TOC]
```
#专有名词缩写
AF：atrial fibrillation  房颤
AFL：atrial flutter  房扑
PAB：房早
AT：房速
PVC：室早
VT：室速
VFL：室扑
VF：室颤
灵敏度：真检测为真的比例
特异度：假检测为假的比例
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
#3.Detecting Atrial Fibrillation and Atrial Flutter in Daily Life Using Photoplethysmography Data(<font color='red'>重要论文</font>)
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
<font color='red'>pNN40 pNN70是什么？
心率变异性(HRV)指标的一种，代表R-R间期与平均R-R间期大于40MS，70MS的个数占总数的百分比</font>
###特征选择：
+ 二分类
Minimal-Redundancy-Maximal-Relevance (mRMR)最小冗余最大相关法
根据MRMR的特征排序选择1-6个特征，最后根据准确度确定特征

+ 多分类
用随机森林选出特征
#4.受运动伪影干扰 PPG 序列的优质信号提取算法
###类型：仪 器 仪 表 学 报   
核心期刊  
投稿录用比例：	53%
审稿速度：	平均 5.76316 个月的审稿周期
审稿费用：	平均 295 元/篇
版面费用：	平均 717 元/页
###作者：孙 斌1，王成超1，陈建飞2，张永芳1，陈小惠1
###摘要：
为了解决可穿戴设备中，由于运动伪影干扰带来的光电容积脉搏波( PPG) 信号不稳定，导致生理参数计算错误的问题，提出了一种可以在 PPG 序列中提取优质、无干扰信号的算法，该算法具有计算量小、抗干扰能力强的优点。首先对采集到的PPG 序列进行带通滤波和降噪; 之后采用峰度、偏度指标判断是否有运动伪影存在; 然后采用滑窗算法对滤波后的 PPG 信号进行特征提取，寻找主波波峰、重搏波波峰; 最后，采用方差判别法对特征值进行进一步筛选，用于提取连续的无干扰 PPG 信号。设计了波长为 905 和 660 nm 的反射式生理参数计算系统，在系统中实现了该算法，使用采集到的受干扰 PPG 信号进行血氧饱和度和血压计算实验，证明了本算法可以有效提取 PPG 序列中的优质信号，提高了生理参数的计算精度。
###个人总结：
1.滤波0.5-6HZ
2.对每个周期的PPG信号与相邻的2个PPG信号求平均是信号平滑
3.计算峰度![](/images/峰度公式.png)峰度描述了数据总体分布形态的陡缓程度
偏度![](/images/偏度公式.png)偏度描述了信号总体分布的对称性
在不受运动伪影干扰的情况下，PPG 序列中每个周期的波形形态基本相似，信号没有大幅度的跳跃，所以计算出的统计量大致相等; 当PPG 序列受到运动伪影干扰时，信号中存在大量不规则的幅度跳变，波形形态产生变化，上述统计量也会发生变化。
只有当所有统计量同时满足某一个**阈值**时，才可以认为 PPG 信号不受运动伪影的干扰。
Tk= K + a1
Ts= SK + a2
<font color='red'>正常人的可以这样处理，病人的这样处理估计就不行了。</font>
4.滑动窗口（窗口中心点值最大）提取主波波峰和重搏波（窗口长度减半）波峰，记录他们的位置信息（数组下标），将半窗检测出的位置信息剔除得到重搏波位置
5.分别计算主波波峰和重搏波波峰的标准差![](/images/波峰标准差公式.png)，设定**阈值**，判断是否符合要求。
Dy= D + a 式中: Dy表示提取到优质 PPG 信号的对应标准差<font color='red'>这个对应的标准差怎么来的？</font>
###优点：
本文提出的 PPG序列优质信号提取算法与传统算法不同，在进行优质信号提取时，仅需要寻找 PPG 信号的主波峰值、重搏波波峰值以及它们的标准差即可，运算步骤少、计算过程简单，运算速度快，而传统算法需要采用卷积、连乘、累加等操作，运算较为繁琐和复杂
#5.ECG Abnormality Detection from PPG Signal
###期刊类型：2019 IEEE Jordan international joint Conference on electrical  Engineering and imformation
###作者：Malak Fora，Sajidah Al-Hammouri，Awad Al-Zaben
###摘要：
Cardiac Arrhythmia is a serious and common
cardiovascular disease. Electrocardiographic signal (ECG) is
usually used for diagnosis. In addition, multi model signal is
also used to reduce false alarms in detecting abnormalities.
New directions were turned around using
Photoplethysmographic signal (PPG) because of its
tremendous advantages. <font color='red'>This paper presents an algorithm to
detect heart beat abnormalities from PPG signal only (mono
type). This method relies on 11 features extracted from 3
subgroups: 4 features from hemodynamic system frequency
response where each PPG beat was assumed to be the system
output, 5 features were extracted from fitting technique. In
which each PPG pulse was approximated as a mixture of
Poisson function. Moreover, 2 features were related to time
domain-properties. </font>This algorithm was tested and evaluated
using MIMIC and MIMIC III databases. Features were then
classified using <font color='red'>Random forest tree and k-nearest neighbors
(KNN) classifiers</font>, promising results were obtained from both
with values of 99% , 95% for accuracy, precision respectively.
本文提出了一种方法：仅从PPG信号中检测心律不齐。11个特征：4个来自血流动力学频率响应。
（频率响应：系统信号的振幅和相位受频率变化而变化的特性就叫频率响应。作用：根据频率响应可以比较直观地评价系统复现信号的能力和过滤噪声的特性。）
从拟合技术中提取5个特征，其中每个PPG脉冲近似认为一个泊松函数的混合。
2个特征与时域特性相关。
###作者总结：
Arrhythmia detection based on features extracted from
PPG signal is presented in this paper. Features were derived
from three main groups. These are: frequency response of
the hemodynamic system under the assumption it is linear
and time invariant (imaginary part mean squared error, STD
of the real fitted part and the peak locations for the absolute
value for both of them), statistical features of PPG's beat
Poisson fitting (mean of occurrences for each Poisson in
addition to the mean and variance for the fitted PPG beat)
and PPG time domain-related features (PPG beat and minmax
lengths). Impressing statistical performance results were
obtained from random forest and KNN classifiers, with
superiority to the first type. Further features and
classification methods are open for future studies in addition
to studying the effect of other physiological states (other than
arrhythmia) on PPG signal.
提出了一种基于PPG信号特征提取的心律失常检测方法。
特征来源于3个主要类群。
1.假设线性和时间不变的血流动力学系统频率响应（虚部均方差，实部拟合的标准差和二者峰值位置的绝对值）
2.PPG节拍的泊松拟合的统计特征（）
3.PPG时域相关特征（PPG节拍和极小长度）
###方法：
根据信号的梯度变化找到一个PPG周期的起始点和结束点，以及波峰位置。
输入（ECG）G(w)->血流动力学系统（转换）Z(w)->输出（PPG）P(w)
假设输入的心跳节拍为高斯脉冲和PPG节拍的同步
高斯脉冲![](/images/高斯脉冲公式.png)
其中μ，δ²为高斯脉冲的均值和方差。均值为PPG信号的波峰点的均值，方差为PPG信号波峰与波谷的方差
在频域中，系统的频率响应=PPG信号的傅里叶变换/输入的高斯脉冲的傅里叶变换
冲Z(w)中提取4个特征：
实部和虚部的峰值绝对值，实部你合成正态分布后的标准差，虚部与0的偏差
对于每个PPG节拍，表示为3个泊松分布的总和
![](/images/ppg泊松分布总和.png)
k:一个节拍期间的时间索引数组
n:泊松分布的总数，这里n=3
ρi:每个泊松分布的概率质量函数（pf，如下）
![](/images/ppg泊松分布.png)
λi是ρi的平均出现次数<font color='red'>没看懂</font>

#6.小波变换结合快速傅里叶变换从 PPG中提取呼吸率
###期刊：
DOI：10．3969~．issn．1005—202X．2016．01．009
###作者：赵素文，高凡，邓莉
###摘要：
应用小波变换对PPG信号进行9层分解，将第9层细节信号和第8层细节信号分解得到的近似信号重建后相加得到呼吸波，然后用改进的快速傅里叶变换频率估计方法从该呼吸波信号中提取呼吸率。用该法从30个PPG样本中提取呼吸率，并将所提取的呼吸率与温度传感器获得的呼吸率用Bland．Altman法进行对比，得到了两者具有良好一致性的结论。
###个人理解：
<font color='blue' size="5">本文可作为中文论文的模板。</font>
PPG信号0.1-0.4Hz为呼吸波信息，通过作者的信号分解过程理解了怎么提取需要的波。先分解，再讲所属频率的波信号相加。
#7.基于光电容积脉搏波描记法的 无创血红蛋白浓度检测技术的研究
###期刊：博士论文
###作者：彭福来
###方法：（主要关注了滤波的方法）
+ 1.物质对光吸收的Lambert-Beer 定律
+ 2.滤波的评价标准：信噪比、均方根误差
+ 3.噪声的消除
    + 3.1高频噪声的消除
    目前比较常用的方法包括：有限脉冲响应（FIR）滤波，无限脉冲响应（IIR）滤波，滑动平均滤波等，这几种滤波实现简单，计算量小，目前比较常用。还有一些其他的基于时频分析、高阶统计量以及基于波形形态的滤波算法，如小波变换、经验模态分解（EMD）算法、独立成分分析（ICA）以及形态滤波等，这些滤波方法通常计算复杂。
    <font color='blue'>本文采用 FIR 滤波、IIR 滤波以及滑动平均滤波三种方法进行高频噪声的滤除。</font>
    + 3.2运动伪迹的消除
    <font color='blue'>约束独立成分分析（cICA）+自适应滤波相结合</font>
        + 3.2.1 信号高频噪声滤波得到信号1
        + 3.2.2 信号1自相关得到周期信息，根据周期信息产生参考信号
        + 3.2.3 将信号1和参考信号经cICA算法得到不含运动干扰的信号2（丢失了幅度信息）
        + 3.2.4 信号2作为输入，信号1作为期望，恢复信号幅度信息，得到经过处理的PPG信号 
    ![](/images/iCIA流程图.png)
    + 3.3 基线漂移的消除
        + 3.3.1 中值滤波器
            对长度为N（奇数）的窗口数据的中值去除
        + 3.3.2 小波变换
            用coif5小波分解，第7层的逼近系数置零，其他层重构
        + 3.3.3 希尔伯特-黄 变换
            主要包括经验模态分解（EMD）和希尔伯特变换两部分。信号首先经 EMD 分解成一组频率独立的振荡信号（本征模态函数 IMF），然对各 IMF 进行希尔伯特变换求出瞬时频率和瞬时相位。与小波变换相比，经验模态分解更适合处理非平稳信号，例如 PPG 等生理信号。
            计算各 IMFs 的平均瞬时频率，将频率小于 0.5 Hz 的成分置零，然后对处理后的各 IMFs 重构原信号，得到去除基线漂移的 PPG 信号。
#8.Motion Artifact Reduction in Photoplethysmography Using Independent Component Analysis
###作者：Byung S. Kim and Sun K. Yoo*
###期刊：IEEE TRANSACTIONS ON BIOMEDICAL ENGINEERING, VOL. 53, NO. 3, MARCH 2006
###摘要：
In
this paper, the motion artifacts were reduced by exploiting the quasi-periodicity
of the PPG signal and the independence between the PPG and the
motion artifact signals. The combination of independent component analysis
and blockinterlea ving with low-pass filtering can reduce the motion
artifacts under the condition of general dual-wavelength measurement
本文利用ppg信号的准周期性和ppg信号与运动伪影信号的独立性，减少了运动伪影。将独立分量分析和分块分析与低通滤波相结合，可以减少一般双波长测量条件下的运动伪影。
###方法：（块交织）
预处理和ICA
预处理包括：周期检测，块交织，低通滤波，反块交织
利用自相关估计出信号周期
块交织：将每个周期对应的取样位置点重新排列（如：N个ppg周期由100个点组成）
N1(1),N2(1)....组成第一个数组
N1(2),N2(2)....组成第二个数组
...
N1(100),N2(100)...组成第100个数组
$$
 \left[
 \begin{matrix}
   N1(1) & N1(2) & N1(3) & \cdots &N1(100) \\
   N2(1) & N2(2) & N2(3) & \cdots &N2(100) \\
   \vdots & \vdots & \vdots & \ddots & \vdots \\
   N100(1) & N100(2) & N100(3) & \cdots &N100(100) \\
  \end{matrix}
  \right]\tag{原矩阵}
$$
即将矩阵转置
<font color='blue'>
病人的信号怎么处理？（个人理解）
    1.取样（2100个点取1000个点）
    2.映射，归一化
</font>
Hence, the low frequency components
and the high frequency components in block interleaved samples
are associated with the synchronized samples (periodic PPG signal)
and the nonsynchronized samples (noise), respectively
个人理解：
对应的点变化小，频率低，说明信号越有周期性，即PPG信号，否则频率高，变化大，对应噪声信号。

处理后将块交织信号经过低通滤波器，过滤掉高频的噪声，再反交织还原ppg信号。



