![](../img/python3/leetcode-algorithm.jpg)
<hr>

#### Leetcode算法
<hr>

##### 1. 两数之和
题目：给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

( 1 ) 方法1：

通过 range 函数可以遍历 nums 索引获取到 nums
的任意一个元素。两个元素相加等于 target，而同一个元素不能使用两遍，所以在进行组合判断的时候，要用当前元素和后面的所有元素进行加和并判断是否为 target。如果是则返回这两个元素的索引。时间复杂度是 O(n<sup>2</sup>)，空间复杂度是 O(n)
```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        # range函数遍历nums的索引获取到nums的元素
        for i in range(len(nums)):
            # 遍历i索引对应元素的下一个...下一个元素
            for j in range(i + 1, len(nums)):
                # 判断两元素之和是否是目标值target
                if  target == nums[i] + nums[j]:
                    # 满足题意则返回这两个元素的下标
                    return [i, j]
```
( 2 ) 方法2：

借助 enumerate 函数遍历列表获取当前元素和它的索引，将当前元素和索引添加到字典中。当遍历到下一个和该元素的和为 target
的元素时，用 target 减去这个(下一个)元素，将得到(满足题意的)结果和字典中已添加的 key 进行匹配，如果存在这样的 key，则返回这个 key
的索引和当前遍历元素的索引。时间复杂度 O(n)，空间复杂度是 O(n)。
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # 声明一个空字典
        dict1 = dict()
        # enumerate函数遍历数组(列表)
        for index, item in enumerate(nums):
            # 目标值减去当前值是为的判断当前元素对应的元素是否在字典中
            dict_item = target - item
            # 判断当前元素对应的元素是否在字典中
            if dict_item in dict1.keys():
                return [dict1[dict_item], index]
            # 不在字典中就把当前元素和索引放到字典中{当前元素,当前元素的索引}
            dict1[item] = index
```
<hr>

##### 2. 两数相加

<!--回到顶部 start-->
<div style="width: 60px;height: auto;z-index: 99;bottom: 30%;position: fixed;right: 0" id="plug-ins">
    <div style="position: relative;float: right">
        <a target="" href="javascript:;" id="weibo"
           style="display: block;width: 40px;height: 40px;background-color: #c4351b;margin-top: 1px;">
            <img width="22" height="20" src="../img/weibo.png" alt=""
                 style="margin-top: 10px;margin-left: 9px">
        </a>
        <a target="_blank" href="http://wpa.qq.com/msgrd?v=3&uin=3330447288&site=qq&menu=yes" id="qq" style="display: block;width: 40px;height: 40px;background-color:#0e91e8;margin-top: 1px">
            <img width="20" height="20" src="../img/qq.png" 
                 style="margin-top: 10px;margin-left: 10px" alt="点击这里给我发消息" title="点击这里给我发消息">
        </a>
        <a href="javascript:" id="wechat"
           style="display: block;width: 40px;height: 40px;background-color:#01b901;margin-top:1px">
            <img width="22" height="20" src="../img/wechat.png"
                 style="margin-top: 10px;margin-left: 9px">
        </a>
        <a href="javascript:" id="go_top"
           style="display: none;width: 40px;height: 40px;background-color: #b5b5b5;margin-top: 1px">
            <img width="22" height="20" src="../img/top.png" alt=""
                 style="margin-top: 10px;margin-left: 9px">
        </a>
    </div>
</div>
<!--回到顶部 stop-->
<!--左侧广告 start-->
<div style="width: auto;height: auto;z-index: 99;position: fixed;left: 0;top: 70px;" id="google_ads">
        <div>
            <div style="width: 180px;height: auto"></div>
            <!-- Vertical -->
            <ins class="adsbygoogle"
                 style="display:block"
                 data-ad-client="ca-pub-6937898095875663"
                 data-ad-slot="2927491642"
                 data-ad-format="auto"
                 data-full-width-responsive="true"></ins>
            <script>
                (adsbygoogle = window.adsbygoogle || []).push({});
            </script>
        </div>
</div>
<!--左侧广告 stop-->
<!--右侧广告 start-->
<div style="width: auto;height: auto;z-index: 99;position: fixed;right: 0;top: 70px;" id="google_ads">
        <div>
            <div style="width: 180px;height: auto"></div>
            <!-- Vertical -->
            <ins class="adsbygoogle"
                 style="display:block"
                 data-ad-client="ca-pub-6937898095875663"
                 data-ad-slot="2927491642"
                 data-ad-format="auto"
                 data-full-width-responsive="true"></ins>
            <script>
                (adsbygoogle = window.adsbygoogle || []).push({});
            </script>
        </div>
</div>
<!--右侧广告 stop-->