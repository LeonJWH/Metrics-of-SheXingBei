# “摄星杯”2021首届全国智能算法对抗赛攻击赛道的客观机器评分代码

攻击赛道的评分体系由客观机器评分和主观人工评分两部分组成，其中客观机器评分主要包含：攻击性、客观真实性以及和原图的感知距离三部分。

初赛阶段客观机器评分和主观人工评分的权重分别为0.8和0.2，复赛阶段两种评分的权重分别为0.6和0.4。相同分数的，排名按照提交时间先后排名。

## 攻击性

我们直接计算选手提交样本在后台模型上的攻击成功率(Attack Success Rate，ASR)来代表样本的攻击性，这个值在0-1之间。


<img width="141" alt="企业微信截图_1627805779359" src="https://user-images.githubusercontent.com/17867054/127764318-7058ede9-034f-4de1-bf4e-40665cce2f7e.png">

其中x为原始测试样本，y为样本的分类标签，Ϝ(x ̂)为防御模型的输出，x ̂为攻击样本。

## 自然真实度

我们限制选手提交的图像具备自然真实的特性，受GAN等生成模型评价指标Inception Score (IS)、FID、KID等的启发，我们取其中的(Fréchet Inception Distance, FID) 来作为图片自然性指标
<img width="197" alt="企业微信截图_16278058535829" src="https://user-images.githubusercontent.com/17867054/127764360-1da0362b-2cb8-4f25-babe-5d0d3400aa42.png">


## 和原图的感知距离

加入这个指标主要是为了防止选手人为挑选一些和原图极为不相似的网上公开样本作为提交，感知距离是一种比传统SSIM和PSNR等更优的图像一致性度量指标
<img width="198" alt="企业微信截图_1627805879587" src="https://user-images.githubusercontent.com/17867054/127764371-58202c0b-69c6-4ee2-b992-ff600206f707.png">

其中f_0hw^l和f_hw^l分别为以X和X ̂为输入，在VGG的第l层特征，d为某一距离度量指标。score_LPIPS的值需要归一化，计算公式为
<img width="317" alt="企业微信截图_1627805913427" src="https://user-images.githubusercontent.com/17867054/127764391-1ecc7590-b6f9-4f83-bd1d-fc74910abfe0.png">

整体的客观机器打分为：
![image](https://user-images.githubusercontent.com/17867054/127764405-95930038-f281-415a-95bd-80d102a662de.png)

由于大赛的攻击赛道使用的是黑盒攻击模式，本仓库只提供FID和LPIPS指标的评分代码，参赛选手可下载这部分评分代码以供参考，用于本地调试攻击模型和算法。

关于大赛的全部评分规则，详情请见比赛官网：

“摄星杯”2021首届全国智能算法对抗赛()

DCLab平台比赛详情地址()
