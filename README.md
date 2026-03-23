# iFlytek-C8hPro-Crack
关于iFlytek C8hPro平板刷机操作的一些研究，很多地方尚有不足之处，在此抛砖引玉，欢迎各位读者开issues与我讨论。
### **iFlytek C8hPro刷机笔记**

**免责声明：**
1. 本项目仅供学习安卓玩机技巧，如果你的平板是课堂版或还需要用于学习，请退出本教程。
2. 本教程涉及解BL锁，刷机等操作，有一定风险。你必须有足够的心理预期，并且确保自己有独自承担一切损失的能力，否则请退出本教程。
3. 如果您未同意此条款或者未遵守本文第2条规定并因此带来的各种经济损失，精神损失，此文章编写者概不负责。
4. 若您不同意以上条款，请您退出并在您的个人设备上删除此文档并不再操作。
5. 一切最终解释权归文章作者所有。

**下载所需文件（部分文件我已经放在本教程仓库）**
1. 紫光展锐驱动程序
2. spd_dump深刷工具
3. 获取读写权限的fdl文件
4. 解BL锁所需要的相关文件
5. 刷入平板的原生/类原生GSI

**一. 解除BL锁**
1. 打开平板的深刷模式并连接电脑：将设备关机，打开深刷工具spd_dump.exe，在关机之后摁住音量减键，并将设备插入计算机，如能看到BROM＞字样，即可松开按键。
如果你在之后的操作中平板出现无限重启或黑屏无法启动的情况，请打开深刷工具spd_dump，按住音量减键和电源键15秒，即可连接电脑。
2. 推送fdl文件：在BROM>出现后输入如下内容并回车：`fdl fdl1.bin所在路径\fdl1.bin 0x5500`。
出现FDL1>后请输入如下内容并回车：`fdl fdl2.bin所在路径\fdl2.bin 0x9efffe00`。
回车接着输入并回车：`exec`。
现已经进入读写模式并显示FDL2>。
3. 备份全盘（重要！）：输入`r all`以备份系统内除userdata分区的所有文件，下载的文件保存在spd_dump目录下。
4. 将解锁BL的文件刷入uboot和splloader分区：准备好解BL锁文件（splloader_c8hpro_disverify.bin和uboot_c8hpro_unlock.bin），在FDL2>下输入`w uboot uboot_c8hpro_unlock.bin文件路径\uboot_c8hpro_unlock.bin`。
完成后输入`w splloader splloader_c8hpro_disverify.bin文件路径\splloader_c8hpro_disverify.bin`。
刷写完成后输入`e userdata`以清除用户数据分区，如果不清除的话可能会导致卡第一屏。
最后输入`reset`并回车以重启。如果你的平板在开机第一屏左下角显示两行带unlock字样的小字，即说明BL锁已解除。

**二. 刷写GSI**
1. 寻找合适的GSI，下载并妥善保存。
2. 假设你下载的GSI文件名为`system.img`，推送两个fdl文件后在FDL2>下输入`w system system.img文件路径\system.img`。
耐心等待刷写完成后输入`e userdata`和`reset`。你的平板会重启并开始清理数据，稍等片刻就能进入你刷的系统。如果你的平板在刷完系统后出现无限重启或卡第一屏等情况，重新刷回你备份的原系统system.bin即可。

**三. 刷回原系统与回锁BL锁**
1. 将你先前备份的原系统system.bin刷回system分区即可恢复原系统。
2. 回锁BL锁需要将你先前备份的miscdata.bin和uboot.bin重新刷回对应分区，代码此处不再赘述。
