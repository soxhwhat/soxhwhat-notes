# 缺点和前沿
二、Transformer带来的成本增加是巨大的
虽然transformer结构会对CV任务带来一定的精度提升，但同时，使用transformer也需要付出一定代价。仅举几例如下：
1、Transformer模型巨大的参数量将成倍地增加服务器成本以及随之而来的运维难度。
2、Transformer在小数据集上很难训练，极易过拟合，因此训练所需的数据量显著增加。并且，有些业务场景天然难以提供大量数据。
3、Transformer的训练时间长，相比CNN，transformer有时甚至需要3~5倍的训练时间，这一方面阻碍了许多需要快速响应的需求的开发（例如某些热点事件的跟进），同时也隐形地增加了公司的人力成本（阿里的算法工程师工资可是很高的哟）。

- 虽然在几个常用benchmark上提升明显，但是在某些实际项目的落地中发现可能还不如vit好用，或者需要精细调参，这个在resnet中是不存在的；

- 整个模型设计，我认为并没有真正从原理上真正解决cnn和vit之间的问题。transformer放在cv两个问题，local feat无法专注，长序列导致显存炸裂。swin采用的local self attention等于是套着cnn的模式到了transformer中，后面接一个shift window，我理想当中应该是采用一种全新的attention设计去解决这两个问题，我甚至有点好奇把local self attention替换一个普通卷积会怎么样。再者就是shift window那一步略显复杂，毕竟simple is best。

- 计算损耗就不多说了，显存这块要求是很高的，平民组不知道能不能玩。

这些成本增加能否接受，则取决于应用该技术的业务是否具有足够的价值了。国内各大互联网公司中，都有transformer的落地先例，例如阿里的搜索推荐、美团的搜索排序、腾讯的广告推荐等。这些无一不是能够带来巨大商业价值的应用场景，在其中取得很小的精度提升，就可以cover相应的改造成本。能否找到类似价值体量的应用场景，也许是transformer能否顺利落地在CV领域的关键。

# 优势
- 首先，transformer对long sequence的建模优势就不说了，CNN在这块是天然的劣势。但transformer目前带来的精度提升，既来自self-attention的理论优势，也不能否认模型参数规模的贡献。
- Transformer真的像变形金刚，只要数据到位、训练到位，模型泛化效果超乎想象。